# CalT
To help you lose weight
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Smart Calorie Tracker</title>
<style>
  body { font-family: Arial, sans-serif; margin: 30px; background: #f2f2f2; }
  h1 { text-align: center; }
  .meal-form, .meal-table { margin: 20px auto; max-width: 600px; }
  input, select, button { padding: 10px; margin: 5px; }
  table { width: 100%; border-collapse: collapse; margin-top: 20px; }
  th, td { border: 1px solid #ccc; padding: 8px; text-align: center; }
  th { background: #eee; }
  .total { font-weight: bold; }
</style>
</head>
<body>

<h1>Smart Calorie Tracker</h1>

<div class="meal-form">
  <select id="mealType">
    <option value="Breakfast">Breakfast</option>
    <option value="Lunch">Lunch</option>
    <option value="Dinner">Dinner</option>
    <option value="Snack">Snack</option>
  </select>
  <input type="text" id="foodName" placeholder="Food Name">
  <input type="number" id="foodQty" placeholder="Quantity (grams)">
  <button onclick="addFood()">Add</button>
</div>

<div class="meal-table">
  <table id="calorieTable">
    <thead>
      <tr>
        <th>Meal</th>
        <th>Food</th>
        <th>Quantity (g)</th>
        <th>Calories</th>
      </tr>
    </thead>
    <tbody>
    </tbody>
    <tfoot>
      <tr>
        <td colspan="3" class="total">Total Calories</td>
        <td id="totalCalories" class="total">0</td>
      </tr>
    </tfoot>
  </table>
</div>

<script>
  // Simple food database (calories per 100g)
  const foodDatabase = {
    "Oatmeal": 190,
    "Chicken Breast": 165,
    "Almonds": 570,
    "Apple": 52,
    "Rice": 130,
    "Egg": 155
  };

  let totalCalories = 0;

  function addFood() {
    const mealType = document.getElementById("mealType").value;
    const foodName = document.getElementById("foodName").value;
    const foodQty = parseFloat(document.getElementById("foodQty").value);

    if (!foodName || !foodQty || foodQty <= 0) {
      alert("Please enter valid food and quantity!");
      return;
    }

    const caloriesPer100 = foodDatabase[foodName];
    if (!caloriesPer100) {
      alert("Food not in database! Add it later or choose another.");
      return;
    }

    const calories = (caloriesPer100 * foodQty) / 100;
    totalCalories += calories;

   