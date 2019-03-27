# GraphQL Services
### Because You Need Another Thing

---?image=assets/img/gql.svg
@title[What is it]

## What is it

@ul[spaced text-black]
- Yes, a 'query language' (**specification**)
- BUT, also a specifiation for `commands` (**mutations**)
- It explicitly defines the _capabilities_ of your application
- BUT, doesn't infect your application with its opinions
@ulend

---

@title[Plays With Others]

## My REST API root
```
GET /app-store-bff/api
Host: team.invisionapp.com
200 OK
{
  "studiogql_url": "https://something.com/studio/gql",
  "webgql_url": "https://another.com/gql"
}
```

## My GraphQL endpoint
```
POST /studio/gql
Host: team.invisionapp.com
{
  "query": "query app($selfUrl: String!){ app(selfUrl: $selfUrl) { name, description} }",
  "variables": {
    "selfUrl": "https://something.com/apps/cjs3hjr8o00080169mv6d1yin/accessibility-analyzer/0.4.0"
  }
}
200 OK
{
    "data": {
        "app": {
            "name": "accessibility-analyzer",
            "description": "The Accessibility Analyzer helps our users design accessible products by analyzing a Studio file to see if it meets W3C accessibility guidelines. A11y Analyzer currently checks contrast ratios between text and backgrounds, minimum text sizes, and minimum line heights.",
            ...
        }
    }
}
```

---?gist=mnichols/3b94f868c5744f4df0d9c1055deecc48&title=Meet The Schema

@title[Meet The Schema]

@[66-71](Query API)
@[134-137](Commands API)
@[53-58](Types)
@[127-132](Inputs)
@[11-16](Enums)

---?image=assets/img/presenter.jpg

@snap[north span-100 headline]
## Now It's Your Turn
@snapend

@snap[south span-100 text-06]
[Click here to jump straight into the interactive feature guides in the GitPitch Docs @fa[external-link]](https://gitpitch.com/docs/getting-started/tutorial/)
@snapend
