# JS-WITH-ME 
## La question est comment organiser et rendre notre code bien lisible et compréhensible ?
## Ou plutôt comment utiliser les routes en Node.js ?

### Premièrement, regardons comment organiser notre fichier.

#### 1. Par exemple, ici dans mon projet, je travaille avec deux fichiers pour le produit et l'authentification. L'architecture doit être comme suit :


<pre/>project/
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
└── package.json</pre>
#### commencons par expliquer ce que contient chaque dossier :
##### dabord controller/ :
ici on a les fichiers ou on met les fonctions callback de notre code , quon a tendance a utiliser dans les routes (app.post(...) , app.put(...) )
la syntaxe comme suit : 
```js
exports.LeNomDeMaFonction = async (req, res) => {
    try {
      const { username, password } = req.body;
      const hashedPassword = await bcrypt.hash(password, 10);
      const user = new User({ username, password: hashedPassword });
      await user.save();
      res.status(201).json({ message: 'Utilisateur enregistré avec succès' });
    } catch (error) {
      res.status(500).json({ error: 'Erreur lors de l\'inscription' });
    }
}
```


de preference on utilise cette syntaxe la au lieu de creer une constante puis l'exporter.

##### ensuite models/ :
dans ces fichiers on met notre schema et on cree notre modele :
```js
const mongoose= require('mongoose')
const MonProductSchema = new mongoose.Schema({
    name: String,
    description: String,
    etc
});
const Product = mongoose.model('Product', MonproductSchema);
module.exports = Product

```
Dans ce fichier, nous définissons le schéma du produit à l'aide de mongoose.Schema. Ensuite, nous créons un modèle de produit en utilisant mongoose.model, en spécifiant le nom du modèle (dans ce cas, "Product") et le schéma correspondant. Enfin, nous exportons ce modèle pour pouvoir l'utiliser dans d'autres parties de notre application.
Enfin, routes/ :

Dans ce dossier, nous définissons les routes de notre application, en associant chaque route à une fonction de contrôleur appropriée. Par exemple, dans productRoutes.js, nous aurions quelque chose comme ceci :
```js
const express = require('express');
const router = express.Router();
const productController = require('../controllers/productController');

// Route pour récupérer tous les produits
router.get('/', productController.getAllProducts);

// Route pour récupérer un produit par son ID
router.get('/:id', productController.getProductById);

// Route pour créer un nouveau produit
router.post('/', productController.createProduct);

// Route pour mettre à jour un produit existant
router.put('/:id', productController.updateProduct);

// Route pour supprimer un produit
router.delete('/:id', productController.deleteProduct);

module.exports = router;
```
Dans ce fichier, nous importons d'abord express et créons un routeur avec express.Router(). Ensuite, nous associons chaque route HTTP (GET, POST, PUT, DELETE) à une fonction de contrôleur spécifique définie dans productController.js. Enfin, nous exportons le routeur pour pouvoir l'utiliser dans notre fichier app.js (ou server.js).
