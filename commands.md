## Parte1 

db["Voice-actors"].find({Edad: {$gt: 50}}, {_id: 0, Nombre: 1, Edad: 1,  }).sort({Edad: 1}).limit(10)
db["Voice-actors"].find({Idiomas: "Inglés", Nacionalidad: "Reino Unido"}, {_id: 0, Nombre: 1, Idiomas: 1, Nacionalidad: 1  }).sort({Nombre: 1}).limit(10)
db["Voice-actors"].find({Edad: {$lt: 30}, Personajes: { $elemMatch: { Rol: "principal", Generos: "Acción"}}}, {_id: 0, Nombre: 1, "Personajes.Rol": 1, "Personajes.Generos": 1, Edad: 1}).sort({Nombre: 1}).limit(10)
db["Voice-actors"].aggregate([{$sort: {Patrimonio: -1}}, {$skip: 4}, {$limit:10}, {$project: {Nombre: 1, Patrimonio: 1, Edad: 1}}])

## Parte2
db["Voice-actors"].find({Edad: {$gt: 50}}, {_id: 0, Nombre: 1, Edad: 1,  }).sort({Edad: 1}).limit(10).explain("executionStats")
db["Voice-actors"].find({Idiomas: "Inglés", Nacionalidad: "Reino Unido"}, {_id: 0, Nombre: 1, Idiomas: 1, Nacionalidad: 1  }).sort({Nombre: 1}).limit(10).explain("executionStats")
db["Voice-actors"].find({Edad: {$lt: 30}, Personajes: { $elemMatch: { Rol: "principal", Generos: "Acción"}}}, {_id: 0, Nombre: 1, "Personajes.Rol": 1, "Personajes.Generos": 1, Edad: 1}).sort({Nombre: 1}).limit(10).explain("executionStats")
db["Voice-actors"].explain("executionStats").aggregate([{$sort: {Patrimonio: -1}}, {$skip: 4}, {$limit:10}, {$project: {Nombre: 1, Patrimonio: 1, Edad: 1}}])

db.getCollection("Voice-actors").createIndex({ Nacionalidad: 1 })
db.getCollection("Voice-actors").createIndex({ Edad: 1 })

## Parte3
db["Voice-actors"].updateMany({Edad: {$lt: 40}}, {
  $push: {Personajes: { NombrePersonaje: "Adagio", Produccion: "Shangrila", TipoProduccion: "profesional", Rol: "principal", CantidadApariciones: 3, Generos: ["Romance"]}},
  $mul: {Patrimonio: 1.32}
},)

db["Voice-actors"].updateMany({Edad: {$gte: 40}}, {
  $push: {Personajes: { NombrePersonaje: "Nature of Daylight", Produccion: "Paltra", TipoProduccion: "profesional", Rol: "secundario", CantidadApariciones: 1, Generos: ["Romance"]}},
  $mul: {Patrimonio: 1.32}
},)