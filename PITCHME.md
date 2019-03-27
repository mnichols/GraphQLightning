---?image=assets/img/gql.png&size=contain
# GraphQL Services
### Because You Need Another Thing

---?image=assets/img/gql.png&size=contain
@title[What is it]

## What is it

@ul[spaced text-black]
- Yes, a 'query language' (**specification**)
- BUT, also a specification for `commands` (**mutations**)
- It explicitly defines the _capabilities_ of your application 
  - Verbs are first-class
  - Discovery is done via the graph, not links
- BUT, doesn't infect your application with its opinions
@ulend

---

## Why reach for _any_ spec

#### Lucene, GraphQL, Structured Query Language, etc...

@ul[spaced text-black]
- Velocity: Learning the lang is faster than rolling your own
- Maintainability: Change is better planned using a Battle-tested spec
- Tooling: A common spec often means community tooling explosion
@ulend

---

@title[Existing API and Avoiding Corners]

@snap[north-west]
General Questions For Adopting Any Specification
@ul[spaced text-black]
- **Integration** : Can it be hosted alongside my other APIs?
- **Age** : Can I change my mind later or will I experience vendor lock-in?
- **Isolation**: Do related dependencies stay isolated from my domain?
- **Iteration**: Can I slowly migrate toward its adoption, or does it force a rewrite?
- GraphQL => **YES!**
@ulend

---

@title[Plays With Others: REST API Root]

**My REST API root**

```json

GET /app-store-bff/api
Host: team.invisionapp.com

200 OK
Content-Type: application/json
{
  "studiogql_url": "https://team.invisionapp.com/studio/gql",
  "webgql_url": "https://team.invisionapp.com/web/gql"
}

```

---
@title[Plays With Others: GraphQL Endpoint]

**My GraphQL endpoint**

```json

POST /studio/gql
Host: team.invisionapp.com
{
  "query": "query app($selfUrl: String!){ app(selfUrl: $selfUrl) { name, description} }",
  "variables": {
    "selfUrl": "https://something.com/apps/cjs3hjr8o00080169mv6d1yin/accessibility-analyzer/0.4.0"
  }
}

200 OK
Content-Type: application/json

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

---

@title[Cons]
#### Cons
```
mutation submitApp($manifest: ManifestInput!, $installStrategies: [InstallStrategy!]!){ submitApp(manifest: $manifest, installStrategies: $installStrategies, team: null) { pending, submitted { key, url }, uploaded } }
```
@ul[spaced text-black]
- Client: Simple clients that don't use something like Apollo need to manually craft the lang
- @size[0.75em](Server: Instrumentation dependent on http status is _different_ {not necessarily worse} since everything is a `POST => OK`)
- Errors are always `200`. Maybe not a **con** but at least a **hmm**.
- Graphs can get complex quickly (they abstract a composition of underlying resources).
  - This can lead to latency if you arent careful
@ulend

---

@title[Pros 1]

#### Pros

> Less "back and forth" cobbling objects together for a client model - Happy Developer.

---

@title[Pros 2]
#### Pros

@ul[spaced text-black]
- Client: Negotiation was simplified because of the inherent Document Driven Design
- Server: Less time writing clever searches over my API that composes _n_ objects.
- Everything is explicit
  - Pagination typically employs `Connections`, an explicit affordance for client pagination details
- Implementation that meets the contract is not mandated by the spec.
@ulend

---?image=assets/img/gql.png&size=contain
@title[GoLang 1]

@snap[north]
### GoLang and Boilerplate
@snapend

@snap[midpoint]
@size[1em](GQLGEN : `https://gqlgen.com/`)
@snapend

---

@title[GoLang 2]

@snap[north-west span-100]
@size[0.5em](GQLGEN : `https://gqlgen.com/`)
<hr />
@snapend

@snap[west small]
@ul[text-black]
- Static types. No `interface{}`.
- Inspects the `schema.graphql` file I showed earlier
- Generates the models, validation, http handler, and resolver interface code for enforcing the spec.
- Exposes smart interfaces for meeting the contracts
- `Resolvers` are the heart of behavior
  - GQLGen provides the interface - you provide the implementation.
- :( Breaking changes occasionally but well maintained
- Sample project at `https://github.com/InVisionApp/gql`
@ulend
@snapend

@snap[south span-100]
@size[0.5em](Blog post @ `GraphQL : Getting Started and Patterns for golang services`)
@snapend

---

@title[Thanks]

@snap[north span-100 headline]
# Thanks for listening
#### Questions? Comments?
@snapend
