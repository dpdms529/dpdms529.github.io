---
layout: single
title: "[Jekyll 블로그] Github Actions로 배포"
excerpt: ""
date: "2023-05-23 21:50:00"
toc: true
toc_sticky: true
use_math: true
categories: [Experiences, Jekyll 블로그]
tags: [Experiences, Jekyll 블로그]
---

## Github Actions
[이전 포스트](https://dpdms529.github.io/experiences/jekyll-%EB%B8%94%EB%A1%9C%EA%B7%B8/Jekyll-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EC%83%9D%EC%84%B1/#github-pages%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EC%A7%80-%EC%95%8A%EC%9D%80-%EC%9D%B4%EC%9C%A0)에서 설명했다시피 블로그의 변경사항을 자동 배포하기 위해 [Github Actions](https://github.com/features/actions)를 사용해보려한다.

1. Actions 탭에 들어가서 `set up a workflow youself`를 클릭한다.

    ![Github Actions](https://github.com/dpdms529/dpdms529.github.io/assets/60471550/eaeba9d4-6f1b-4b83-bfb1-17c60387e45d)

2. 파일명을 `github-pages`로 하고 내용을 다음과 같이 작성한다.

    ![github-pages.yml](https://github.com/dpdms529/dpdms529.github.io/assets/60471550/c9321d3d-571f-4c93-be9f-dd7467c4752f)

    ```yml
    name: Build and deploy Jekyll site to GitHub Pages

    on:
    push:
        branches:
        - main

    jobs:
    github-pages:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v3
        - uses: actions/cache@v2
            with:
            path: vendor/bundle
            key: ${{ runner.os }}-gems-${{ hashFiles('**/Gemfile') }}
            restore-keys: |
                ${{ runner.os }}-gems-
        - uses: helaili/jekyll-action@2.5.0
            with:                                
            token: ${{ secrets.JEKYLL_TOKEN }}
            target_branch: 'gh-pages'
            pre_build_commands: 'gem update --system'
    ```
    
    위와 같이 설정하면 `main`브랜치에 변경 사항이 생겼을 때마다 `main` 브랜치의 내용으로 정적인 페이지들을 만들어서 `gh-pages` 브랜치에 올려준다.

3. <https://github.com/settings/tokens> 에서 `Generate new token`을 한 후 Note에는 `JEKYLL_TOKEN`를 입력하고, Expiration은 `No expiration`, Select scopes는 `public_repo`를 선택해준다.

    ![token 설정](https://github.com/dpdms529/dpdms529.github.io/assets/60471550/efe70843-59d3-4531-b63d-23caf3a1dcf3)

4. 생성된 token 값을 복사해준다.

    ![token 생성](https://github.com/dpdms529/dpdms529.github.io/assets/60471550/0b999a41-edfd-434b-870e-7bb0a0653102)

5. 레포지토리로 돌아와서 `Setting`의 `Secrets and variables`에 들어가서 `New repository secret`으로 위에서 만들었던 `JEKYLL_TOKEN`을 secret으로 등록해준다.

    ![secret 등록](https://github.com/dpdms529/dpdms529.github.io/assets/60471550/7224431f-819e-4a89-877d-d9b3b8957afe)

    ![secret 설정](https://github.com/dpdms529/dpdms529.github.io/assets/60471550/476313b7-fc42-4e8d-b1c3-7c6443b80e98)

6. 지금까지의 변경사항을 모두 `commit` 후 `push` 해주면 `Actions`의 `workflow`에 commit한 내용이 올라가고 `gh-pages`라는 브랜치가 생성된다. 

    ![workflow](https://github.com/dpdms529/dpdms529.github.io/assets/60471550/20fdb4b6-23d8-4b6f-babc-86406ea31cde)

    ![gh-pages](https://github.com/dpdms529/dpdms529.github.io/assets/60471550/64d6b8f4-de76-48ce-a8e9-b0f569224e73)

7. `Settings`의 `Pages`에 들어가서 배포할 브랜치를 `gh-pages`를 변경해준다.
    
    ![Pages 설정](https://github.com/dpdms529/dpdms529.github.io/assets/60471550/05b14c12-219e-48ed-a522-d60271d18f1d)

8. `https://<사용자이름>.github.io/`로 접속하면 Github Pages로 블로그가 호스팅되고 있는 것을 확인할 수 있다.