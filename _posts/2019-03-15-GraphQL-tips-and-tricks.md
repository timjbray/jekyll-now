---
layout: post
title: GraphQL tips and tricks.
---

We're using the awesome [Apollo](https://www.apollographql.com) client and server libraries. They've been reliable, full featured and (mostly) easy to use - albeit with reasonable learning curve. Here are a few items that we didn't immediately see in the documentation (which is generally very good), or found we needed during development and roll out to production.


# GraphQL vs the libraries

The Apollo libraries do a log of heavy lifting for you. This makes it easy to get started, but with this help and abstraction you can easily get lost as to what the libraries are doing and what is just GraphQL. 

### GraphQL Playground 

The [playground](https://www.apollographql.com/docs/apollo-server/features/graphql-playground.html) is invaluable in playing around with queries and mutations. Add your `Authorization` HTTP header to query anything that is not public. 

```
{
  "Authorization": "Bearer eyJhbGciOiJIUzI....."
}
```
### Chrome dev tools

For further debugging head to Chrome's network tools. You can see the full request and response, then copy the request as `cURL` and directly import into the great [Postman](https://www.getpostman.com) API editor for further debugging.

![graphql_chrome_tools]({{ site.baseurl }}/images/graphql-chrome-dev-tools-copy.png)

### Raw GraphQL

These tools make it easy to get comfortable with the language by viewing and testing GraphQL. You can then write queries or mutations without using the client libraries. 

For example, here we're calling a mutation using plain JS. 

```js
const refreshToken = apiUri => () => {
  return fetch(apiUri, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      operationName: 'authRefreshToken',
      query: `mutation authRefreshToken {
                authRefreshToken {
                  ok
                  access_token
                }
              }`
    })
  })
    .then(res => res.json())
    .catch(error => console.log(error.message));
};
```

# Logging

It's essential to log errors and requests. We found with the default setup, syntax errors and other issues became hard to debug unless we riddled our code with exception handling. We then found this [feature](https://www.apollographql.com/docs/apollo-server/features/errors.html#Masking-and-logging-errors) of the Apollo server constructor, which allows logging (& modifying) errors and responses.

```js
const server = new ApolloServer({
  typeDefs,
  resolvers,
  context: graphQLContext,
  formatError: (error: any) => {
    // filter whatever errors your don't want to log
    logger.error(`[GraphQL.error] ${error.message}`, error);
    return error;
  },
  formatResponse: (response: any) => {
    // don't log auth mutations or schema requests
    const name = Object.keys(get(response, 'data') || { unknown: 0 })[0];
    if (!['authSignIn', 'authRefreshToken', '__schema', ... ].includes(name)) {
      logger.debug(`[GraphQL.response] ${name}()`, response);
    }
    return response;
  }
});

```

# Authentication

When starting our project, we initially had all GraphQL operations (API calls) public. We then added auth via Express middleware, and started to pass an `isAuthenticated` flag down to all query and mutation resolvers. 

```js
  async user(_, args, context) {
    if (!context.isAuthenticated) {
      throw new AuthenticationError('Not authenticated.');
    }
    ...
```

While this worked fine, it starts to get very messy as soon as the project started to grow. We then centralised auth into the context using `gql` to parse the incoming operation. The `gql` command takes in the text based operation and returns a GraphQL object - with operation type, operation name, fields (via `selectionSet`) etc.

```js
const server = new ApolloServer({
  typeDefs,
  resolvers,
  context: graphQLContext
});

const graphQLContext = (context) => {
  const { req, res } = context;

  // use a express middleware to auth user
  const isAuthenticated = Boolean(req.user);

  const { name, operation } = getOperationName(req);

  // Check here if this a public operation or not

  return {
    currentUser: req.user,
    isAuthenticated
  };
};

const getOperationName = (req) => {
  const query = req.body.query;
  
  // use gql to parse the given query/mutation
  const op = gql`
    ${query}
  `;

  // this is the name the user gave for the operation
  const operationNameDefault = get(req, 'body.operationName');

  // this is the name of the actual operation
  const name = get(op, 'definitions[0].selectionSet.selections[0].name.value') || operationNameDefault;
  const operation = get(op, 'definitions[0].operation') || '';

  return { name, operation };
};
```


# Querying what fields have been selected

While talking about resolvers and context, one 

https://www.apollographql.com/docs/graphql-tools/resolvers#Resolver-function-signature

This was something that worried us 
This 


- view the field names requested in the query - only select them (becomes very complex)
- get Operation Name