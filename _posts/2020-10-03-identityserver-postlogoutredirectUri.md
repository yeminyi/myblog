---
layout: post
title: PostLogoutRedirectUri always null in identity Server 4 with Angular OIDC client
categories: IdentityServer4
tags: [identityserver4]
---

## Problem

The LogoutId always was NULL in identity Server 4 when the Angular OIDC client redirect to logout.

## Remove the `post_logout_redirect_uri` setting 

``` typescript

var config = {
        authority: 'http://localhost:4242/',
        client_id: 'spa-client',
        redirect_uri: `http://localhost:4200/oidc-login-redirect.html`,
        scope: 'openid projects-api profile',
        response_type: 'id_token token',
        //*------REMOVE THIS, OTHERWISE THE LOGOUTID ALWAYS NULL  -------*/
        // post_logout_redirect_uri: `${Constants.clientRoot}`,
        //*------REMOVE THIS, OTHERWISE THE LOGOUTID ALWAYS NULL  -------*/       
    }
   
```


  Please refer the link [here](https://stackoverflow.com/questions/53824770/postlogoutredirecturi-always-null-in-identity-server-4-with-spa-angular-7-oidc)