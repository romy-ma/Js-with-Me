# js-with-me 
## la question est comment organiser et rendre notre code bien lisible et comprehensible ?
## ou plutot comment utiliser les routes en node js ?
### premierement allons voir comment va t on organiser notre fichier 
#### 1. par exemple ici dans mon projet je travaille avec deux fichiers pour le produit et lauthentification , larchitecture doit etre comme ca :
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

