# GraphQL : Because You Need Another Thing

---

## What is it

![](assets/img/presentation.png)

---
@title[What is it]

@snap[west span-50]
@ul[spaced text-black]
- Yes, a 'query language' (**specification**)
- BUT, also a specifiation for `commands` (**mutations**)
@ulend
@snapend

@snap[east span-50]
![](assets/img/presentation.png)
@snapend

---?color=#E58537
@title[Meet The Schema]

@snap[north-west]
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

@snap[north-east]
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
