<?php
require 'config.php';

if ($_SERVER["REQUEST_METHOD"] === "POST") {
    $id = $_POST["id"];
    $nom = $_POST["nom"];
    $prenom = $_POST["prenom"];
    $email = $_POST["email"];
    $qualite = $_POST["qualite_produit"];
    $description = $_POST["description"];

    $stmt = $conn->prepare("INSERT INTO produits (id, nom, prenom, e_mail, qualite_produit, description) VALUES (?, ?, ?, ?, ?, ?)");
    if ($stmt) {
        $stmt->bind_param("isssss", $id, $nom, $prenom, $email, $qualite, $description);
        $stmt->execute();
        $stmt->close();
        echo "<p style='color: green;'>Produit enregistré avec succès !</p>";
    } else {
        echo "<p style='color: red;'>Erreur SQL : " . $conn->error . "</p>";
    }
}
?>

<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Formulaire Produit</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #a8edea, #fed6e3);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    .form-container {
      background-color: white;
      padding: 30px;
      border-radius: 15px;
      box-shadow: 0 8px 16px rgba(0,0,0,0.2);
      width: 400px;
    }

    h2 {
      text-align: center;
      margin-bottom: 20px;
      color: #333;
    }

    label {
      font-weight: bold;
      color: #555;
    }

    input, select, textarea {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      margin-bottom: 15px;
      border: 1px solid #ccc;
      border-radius: 8px;
      transition: 0.3s;
    }

    input:focus, select:focus, textarea:focus {
      border-color: #66afe9;
      outline: none;
      box-shadow: 0 0 8px #66afe9;
    }

    button {
      background-color: #ff4081;
      color: white;
      padding: 12px;
      border: none;
      border-radius: 10px;
      font-size: 16px;
      cursor: pointer;
      width: 100%;
      transition: background-color 0.3s ease;
    }

    button:hover {
      background-color: #e91e63;
    }

    .link {
      text-align: center;
      margin-top: 15px;
    }

    .link a {
      text-decoration: none;
      color: #007BFF;
    }
  </style>
</head>
<body>
  <div class="form-container">
    <h2>Ajouter un produit</h2>
    <form method="POST">
      <label for="id">ID :</label>
      <input type="number" id="id" name="id" required>

      <label for="nom">Nom :</label>
      <input type="text" id="nom" name="nom" required>

      <label for="prenom">Prénom :</label>
      <input type="text" id="prenom" name="prenom" required>

      <label for="email">Email :</label>
      <input type="email" id="email" name="email" required>

      <label for="qualite_produit">Qualité de Produit :</label>
      <select id="qualite_produit" name="qualite_produit" required>
        <option value="">--Choisir--</option>
        <option value="neuf">Neuf</option>
        <option value="comme_neuf">Comme neuf</option>
        <option value="assez_bon">Assez bon</option>
        <option value="use">Usé</option>
      </select>

      <label for="description">Description :</label>
      <textarea id="description" name="description" rows="4" required></textarea>

      <button type="submit">Enregistrer</button>
    </form>
    <div class="link">
      <a href="afficher.php">Voir les produits</a>
    </div>
  </div>
</body>
</html>
