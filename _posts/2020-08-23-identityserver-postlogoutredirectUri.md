---
layout: post
title: PostLogoutRedirectUri always null in identity Server 4 with Angular OIDC client
categories: IdentityServer
tags: [identityserver]
---

## Remove the `post_logout_redirect_uri` setting 

``` typescript

var config = {
        authority: 'http://localhost:4242/',
        client_id: 'spa-client',
        redirect_uri: `${Constants.clientRoot}assets/oidc-login-redirect.html`,
        scope: 'openid projects-api profile',
        response_type: 'id_token token',
        //*------REMOVE THIS, OTHERWISE THE LOGOUTID ALWAYS NULL  -------*/
        // post_logout_redirect_uri: `${Constants.clientRoot}`,
        //*------REMOVE THIS, OTHERWISE THE LOGOUTID ALWAYS NULL  -------*/       
    }
   
```


  Please refer the link [here](https://stackoverflow.com/questions/53824770/postlogoutredirecturi-always-null-in-identity-server-4-with-spa-angular-7-oidc)