# Skill: Multi Tenant

Toda consulta y mutación debe quedar limitada por merchantId.
Nunca aceptar merchantId de forma confiable solo desde el cliente: derivar del
contexto autenticado cuando el diseño del proveedor lo permita.
Prueba aislamiento entre comercios.
