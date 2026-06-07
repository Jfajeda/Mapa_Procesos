# AGENTS.md — Mapa_Procesos

> Proyecto #16 del ecosistema CODANOR

## Descripcion

Editor visual de mapas de procesos con 3 capas (Estrategicos / Operativos / Apoyo).
Permite gestionar mapas diferentes por cliente y por norma (ISO 9001, 14001, 27001, 45001, 22301, ENS).

## Stack

- HTML unico autocontenido (`mapa_procesos.html`)
- JavaScript vanilla (drag & drop con Pointer Events API)
- SVG para conexiones/flechas entre procesos
- IndexedDB para persistencia local (clave: clienteId_normaId)
- jsPDF + html2canvas (CDN con SRI) para exportar PDF
- Sin servidor, funciona con file://

## Estructura

```
Mapa_Procesos/
├── mapa_procesos.html    ← Aplicacion principal
├── AGENTS.md             ← Este archivo
├── Memory.md             ← Registro operativo
├── opencode.json         ← Config OpenCode
└── .gitignore
```

## Arquitectura del HTML

### Capas visuales
- **Estrategicos** (azul #0088CC): Planificacion, revision por direccion, mejora continua
- **Operativos** (verde #12A79D): Procesos core del negocio del cliente
- **Apoyo** (gris #6c757d): RRHH, TI, compras, mantenimiento, etc.

### Modelo de datos (IndexedDB)

```javascript
// Object store: "mapas"
// Key: "{clienteId}_{normaId}"
{
  clienteId: "string",
  normaId: "string",  // ISO9001, ISO14001, ISO27001, ISO45001, ISO22301, ENS
  procesos: [
    {
      id: "uuid",
      nombre: "string",
      capa: "estrategico|operativo|apoyo",
      x: number, y: number,  // posicion en canvas
      descripcion: "string",
      objetivo: "string",
      responsable: "string",
      recursos: "string",
      indicadores: "string"
    }
  ],
  conexiones: [
    { id: "uuid", origen: "procesoId", destino: "procesoId", tipo: "flujo|dependencia|informacion" }
  ],
  metadata: { creadoEn: "ISO date", modificadoEn: "ISO date" }
}

// Object store: "clientes"
// Key: "clienteId"
{ id: "string", nombre: "string", creadoEn: "ISO date" }
```

### Seguridad
- CSP meta tag incluida
- escapeHtml() para todo texto renderizado desde datos de usuario
- Sin eval(), sin innerHTML con datos no sanitizados
- CDN con integrity + crossorigin

## Normas soportadas

| Codigo | Norma | Procesos tipicos precargados |
|--------|-------|------------------------------|
| ISO9001 | Calidad | Planificacion SGC, Revision direccion, Diseno, Produccion, Compras, RRHH |
| ISO14001 | Ambiental | Politica ambiental, Aspectos ambientales, Requisitos legales, Control operacional |
| ISO27001 | Seguridad Info | Politica SGSI, Gestion riesgos, Control acceso, Gestion incidentes, Continuidad |
| ISO45001 | SST | Politica SST, Evaluacion riesgos, Investigacion incidentes, Preparacion emergencias |
| ISO22301 | Continuidad | Analisis impacto, Estrategias continuidad, Planes continuidad, Ejercicios/pruebas |
| ENS | Seguridad Nacional | Marco organizativo, Marco operacional, Medidas proteccion, Gestion incidentes |

## Branding CODANOR
- Primary: #0088CC (dashboards: #0056b3)
- Accent: #12A79D
- Fonts: Poppins (titulos), Nunito Sans (cuerpo)
- Logo: https://codanor.com/assets/img/logo_web-50.png
