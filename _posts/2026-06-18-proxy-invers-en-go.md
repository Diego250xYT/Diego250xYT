---
title: "Proxy inverso en Go: cuando necesitas algo ligero y rapido"
date: 2026-06-18
---

Hace un par de semanas necesitaba un proxy inverso para unos microservicios
que estoy levantando en un VPS. Nginx es la opción obvia, pero para este
proyecto en particular quería algo más integrado, que pudiera controlar
desde código sin andar tocando archivos de configuración.

Así que me senté un domingo por la tarde con música de fondo y escribí un
proxy inverso en Go. Porque para eso sirve Go: para sentarse y escribir.

## Cómo funciona

Es bastante simple en concepto: recibe peticiones HTTP, revisa el
encabezado `Host`, lo compara contra un mapa de rutas configurado en un
archivo YAML, y redirige el tráfico al backend correspondiente.

```go
type Route struct {
    Host    string `yaml:"host"`
    Backend string `yaml:"backend"`
}
```

Usé `httputil.ReverseProxy` del paquete estándar, que hace casi todo el
trabajo pesado. Solo tuve que implementar el `Director` personalizado para
modificar las URLs y encabezados antes de reenviar.

## Lo bueno

- Binario único, sin dependencias externas.
- Configuración en YAML que se recarga con una señal SIGHUP.
- Logging estructurado a STDOUT.
- Compila en segundos.

## Lo pendiente

Todavía no tiene balanceo de carga ni soporte para WebSockets, pero para
lo que ocupo ahorita funciona perfecto. Si alguien más lo encuentra útil,
lo subo a GitHub con todo y documentación.

El código está en [github.com/Diego250xYT/goproxy](https://github.com/Diego250xYT/goproxy).
