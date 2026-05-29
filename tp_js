# TP JavaScript - Niveau Débutant

## Thème : Système de gestion de colis

---

## 1. Objectif du TP

Ce TP permet d’apprendre les bases de JavaScript à travers un cas simple : la gestion des clients et des colis dans un système de livraison, avec affichage dans une page HTML et utilisation de alert() au lieu de la console.

---

## 2. Exercice 1 : Afficher une liste de clients en HTML

Créer une page HTML et afficher les clients dans l’écran.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>TP Colis</title>
</head>
<body>

<h2>Liste des clients</h2>
<p id="clients"></p>

<script>
const clients = [
  "Jean Dupont",
  "Claire Martin",
  "Lucas Bernard"
];

document.getElementById("clients").innerHTML = clients.join("<br>");
</script>

</body>
</html>
```

---

## 3. Exercice 2 : Ajouter un client avec alert

Ajouter un client et afficher une notification.

```html
<script>
let clients = ["Jean Dupont", "Claire Martin"];

clients.push("Emma Thomas");

alert("Nouveau client ajouté : Emma Thomas");
</script>
```

---

## 4. Exercice 3 : Afficher les colis dans la page

```html
<h2>Liste des colis</h2>
<ul id="colis"></ul>

<script>
const colis = ["COL001", "COL002", "COL003", "COL004"];

let liste = "";
for (let i = 0; i < colis.length; i++) {
  liste += "<li>" + colis[i] + "</li>";
}

document.getElementById("colis").innerHTML = liste;
</script>
```

---

## 5. Exercice 4 : Message de statut avec alert

```html
<script>
let statut = "Livré";

if (statut === "Livré") {
  alert("Le colis a été livré avec succès");
} else {
  alert("Le colis est en cours de livraison");
}
</script>
```

---

## 6. Exercice 5 : Compter les colis et afficher dans la page

```html
<h2>Nombre total de colis</h2>
<p id="total"></p>

<script>
const colis = ["COL001", "COL002", "COL003", "COL004"];

document.getElementById("total").innerHTML = "Total : " + colis.length;
</script>
```

---

## 7. Conclusion

Ce TP permet de maîtriser :

* les tableaux
* les conditions
* les boucles
* l’affichage dans une page HTML
* l’utilisation de alert()

Il remplace la console par une interface simple visible dans un navigateur.
