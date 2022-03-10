# duct.middleware.ring-jwt
[Duct](https://github.com/duct-framework)/[Integrant](https://github.com/weavejester/integrant) keys for wrapping
the [ring-jwt](https://github.com/ovotech/ring-jwt) middleware. 

> **DEPRECATION NOTICE**: This repo is no longer maintained. The canonical repo is the fork that can be found [here](https://github.com/kelveden/duct.middleware.ring-jwt).

## Installation
```
[ovotech/duct.middleware.jwt "1.0.0"]
```

## Usage

Both a duct module and, for more flexibility, an integrant key are provided. Both options take an
option map that is the same as for [ring-jwt itself](https://github.com/ovotech/ring-jwt#usage).

### As a duct module

The Duct module will configure the [ring-jwt](https://github.com/ovotech/ring-jwt) middleware AND will hook it into
your `:duct.handler/root`. i.e.

```clj
{:duct.module/ring-jwt
  {:alg :HS256 :secret "somesecret"}} 
```

will merge in the following config to your Duct configuration:

```clj
{:duct.middleware/ring-jwt
 {:alg :HS256 :secret "somesecret"}
 
 :duct.handler/root
 {:middleware [(ig/ref :duct.middleware/ring-jwt)]}}
```

### As an integrant key

```clj
{:duct.middleware/ring-jwt
  {:alg :HS256 :secret "somesecret"}
```

You will then need to hook it into a handler of your choice in your configuration; e.g.:

```clj
{:duct.handler/root
 {:router     #ig/ref :duct.router/ataraxy
  :middleware [#ig/ref :duct.middleware/ring-jwt]}}
```  
