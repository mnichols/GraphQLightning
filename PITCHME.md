# GraphQL
### Because You Need Another Thing

@snap[south]
![](assets/img/gql.svg)

---
@title[What is it]

## What is it

@ul[spaced text-black]
- Yes, a 'query language' (**specification**)
- BUT, also a specifiation for `commands` (**mutations**)
@ulend

---?color=#E58537
@title[Meet The Schema]

@snap[west span-50]
## Query API

```
type Query {
  app(selfUrl: String!): App!
  apps(criteria: AppsCriteriaInput!): [App!]
  latest(selfUrl: String!): App!
  uploads(name: String!, version: String!): Files!
}
```
@snapend

@snap[east span-50]
## Commands API

```
type Mutation {
  submitApp(manifest: ManifestInput!, installStrategies: [InstallStrategy!]!, team: String): Files!
  verifyApp(selfUrl: String!, status: AppStatus!): App!
}
```
@snapend

---?image=assets/img/presenter.jpg

@snap[north span-100 headline]
## Now It's Your Turn
@snapend

@snap[south span-100 text-06]
[Click here to jump straight into the interactive feature guides in the GitPitch Docs @fa[external-link]](https://gitpitch.com/docs/getting-started/tutorial/)
@snapend
