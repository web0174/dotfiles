## `.gitlab-ci.yml`

```yaml


image: node:lts

pages:
  before_script:
    # Clean public folder
    - find public -mindepth 1 -maxdepth 1 -type d | xargs rm -rf
    - find public -type f -name "*.html" | xargs rm -rf
    # entra in base-blog e installa
    - cd base-blog
    - npm install
  script:
    # builda 
    - npm run build-ghpages
    # torna su
    - cd ..
  artifacts:
    paths:
      - public
  publish: public
  rules:
    - if: '$CI_COMMIT_REF_NAME == "main"'

```


```yml

image: node:lts

pages:
  before_script:
    # Clean public folder
    - find public -mindepth 1 -maxdepth 1 -type d | xargs rm -rf
    - find public -type f -name "*.html" | xargs rm -rf
    - npm install
  script:
    # builda 
    - npm run build
  artifacts:
    paths:
      - public
  publish: public
  rules:
    - if: '$CI_COMMIT_REF_NAME == "main"'

```

## DEPLOY DA CARTELLA DEV

```yml

image: node:lts

pages:
  before_script:
    # Clean deploy folder
    - find dev -mindepth 1 -maxdepth 1 -type d | xargs rm -rf
    - find dev -type f -name "*.html" | xargs rm -rf
    - npm install
  script:
    # build 
    - npm run build
  artifacts:
    paths:
      - dev
  publish: dev
  rules:
    - if: '$CI_COMMIT_REF_NAME == "main"'

```
