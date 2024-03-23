# js.withme
## la question est comment organiser et rendre notre code bien lisible et comprehensible ?
## ou plutot comment utiliser les routes en node js ?
### premierement allons voir comment va t on organiser notre fichier 
#### 1. par exemple ici dans mon projet je travaille avec deux fichiers pour le produit et lauthentification , larchitecture doit etre comme ca :
project/
│
├── controllers/
│   ├── authController.js
│   ├── productController.js
│   └── ...
│
│
├── models/
│   ├── user.js
│   ├── product.js
│   └── ...
│
├── routes/
│   ├── authRoutes.js
│   ├── productRoutes.js
│   └── ...
│
├── app.js (ou server.js)
├── config.js (configuration)
└── package.json
