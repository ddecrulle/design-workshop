# How to deploy Stromae-v2

## The chart

You can found some documentation about the chart [here](https://github.com/InseeFr/Helm-Charts/tree/main/charts/stromae-v2). The chart is designed to deploy the UI, API and a Postgres data base. Off course you can enable only ui, only api, db ...

## Example value for ui deployment

```yaml
ui:
  enabled: true
  nameOverride: stromae-ui
  replicaCount: 1
  image:
    repository: inseefr/stromae
    // highlight-start
    tag: "" // Replace by the version you want
    // highlight-end
    imagePullPolicy: IfNotPresent
  ingress:
    enabled: true
    annotations:
      kubernetes.io/ingress.class: nginx
    hosts:
    // highlight-start
      - host: host.url
    // highlight-end
        paths:
          - path: /
            pathType: ImplementationSpecific
    tls:
      // highlight-start
      - hosts:
          - host.url
      // highlight-end
  env:
    AUTHENTICATION_TYPE: NONE
```

<details>

<summary>Example values for ui, api and database</summary>

:warning: This values are for development only (no authentification, cors ...)

```yaml
  ui:
  enabled: true
  nameOverride: stromae-ui
  replicaCount: 1
  image:
    repository: inseefr/stromae
    // highlight-start
    tag: "" // Replace by the version you want
    // highlight-end
    imagePullPolicy: IfNotPresent
  ingress:
    enabled: true
    annotations:
      kubernetes.io/ingress.class: nginx
    hosts:
    // highlight-start
      - host: ui.host.url
    // highlight-end
        paths:
          - path: /
            pathType: ImplementationSpecific
    tls:
      // highlight-start
      - hosts:
          - ui.host.url
      // highlight-end
  env:
    AUTHENTICATION_TYPE: NONE
    API_URL: api.host.url

  api:
    enabled: true
    nameOverride: stromae-api
    replicaCount: 1
    image:
      repository: inseefr/queen-back-office
      // highlight-start
      tag: "" // Replace by the version you want
      // highlight-end
      imagePullPolicy: IfNotPresent
    ingress:
      enabled: true
      hosts:
      // highlight-start
        - host: api.host.url
      // highlight-end
          paths:
            - path: /
              pathType: ImplementationSpecific
      tls:
        - hosts:
            // highlight-start
            - api.host.url
            // highlight-end

    env:
      JAVA_OPTS: -Dlogging.config=${CATALINA_BASE}/webapps/log4j2.xml -Dspring.profiles.active=dev -Dspring.config.location=classpath:/,${CATALINA_BASE}/webapps/queenbo.properties
      #Application configuration
      FR_INSEE_QUEEN_APPLICATION_MODE: noauth
      FR_INSEE_QUEEN_APPLICATION_CROSORIGIN: "*"
      FR_INSEE_QUEEN_PILOTAGE_INTEGRATION_OVERRIDE: true

  postgresql:
    enabled: true
    nameOverride: stromae-postgres
    auth:
      username: usernameDB
      password: passwordDB
      database: stromae-db
      postgresPassword: postgresPasswordDB

```

</details>
