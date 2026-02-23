<template>

<div class="calculator-wrapper">
<div class="calculator-container">


<div class="header">
<div class="icon"> </div>
<h1>Premium Gold & Silver Calculator</h1>
<p>Calculate your jewelry costs with precision</p>
</div>


<form @submit.prevent="calculateTotal" class="calculator-form">
<div class="form-row">
<div class="form-group">
<label for="metal">Select Metal</label>
<select id="metal" v-model="metal" @change="updateRate" class="select-input">
<option value="gold"> Gold</option>
<option value="silver"> Silver</option>
</select>
</div>


<div class="form-group">
<label for="rate">Rate per Gram (₹)</label>
<input id="rate" type="number" v-model.number="rate" step="0.01" placeholder="e.g.,
5000" required class="number-input">
</div>
</div>


<div class="form-row">
<div class="form-group">
<label for="purity">Purity (decimal)</label>


<input id="purity" type="number" v-model.number="purity" step="0.001" min="0" max="1" placeholder="e.g., 0.916" required class="number-input">
<small>22k = 0.916, 24k = 1.000</small>
</div>


<div class="form-group">
<label for="weight">Weight (grams)</label>
<input id="weight" type="number" v-model.number="weight" step="0.01" min="0.01" placeholder="e.g., 10" required class="number-input">
</div>
</div>


<div class="form-group full-width">
<label for="designCharge">Design & Making Charge (₹)</label>
<input id="designCharge" type="number" v-model.number="designCharge" step="0.01" placeholder="e.g., 500" required class="number-input">
</div>


<button type="submit" class="calculate-btn">
<span class="btn-icon"> </span>
Calculate Total Cost
</button>
</form>


<div v-if="total !== null" class="result-card">
<div class="result-header">
<h2> Calculation Result</h2>


</div>
<div class="result-breakdown">
<div class="result-item">
<span class="label">Base Cost:</span>
<span class="value">₹{{ baseCost.toFixed(2) }}</span>
</div>
<div class="result-item">
<span class="label">Tax (12%):</span>
<span class="value">₹{{ tax.toFixed(2) }}</span>
</div>
<div class="result-item total">
<span class="label">Total Cost:</span>
<span class="value">₹{{ total.toFixed(2) }}</span>
</div>
</div>
</div>
</div>

</div>

</template>


<script setup>
import { ref, computed, onMounted } from 'vue'


const metal = ref('gold')
const rate = ref(0)
const purity = ref(0.916) // Default for 22k gold


const weight = ref(1)
const designCharge = ref(0)
const total = ref(null)


const baseCost = computed(() => {
return (rate.value * purity.value * weight.value) + designCharge.value
})


const tax = computed(() => {
return baseCost.value * 0.12
})


const calculateTotal = () => {
total.value = baseCost.value + tax.value
}


const updateRate = () => {
// You can add logic here to fetch current rates if needed
// For now, we'll keep it manual
}


onMounted(() => {
// Initialize with some default values if needed
})
</script>


<style scoped>
.calculator-wrapper {
min-height: 100vh;
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
padding: 2rem 1rem;
display: flex;
align-items: center;
justify-content: center;
}


.calculator-container {
max-width: 700px;
width: 100%;
background: rgba(255, 255, 255, 0.95);
backdrop-filter: blur(10px);
border-radius: 20px;
box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
overflow: hidden;
animation: fadeInUp 0.6s ease-out;
}


@keyframes fadeInUp {
from {
opacity: 0;
transform: translateY(30px);
}


to {
opacity: 1;
transform: translateY(0);
}
}


.header {
background: linear-gradient(135deg, #ffd700 0%, #ffb347 100%);
padding: 2rem;
text-align: center;
color: white;
}


.icon {
font-size: 3rem;
margin-bottom: 1rem;
}


.header h1 {
margin: 0 0 0.5rem 0;
font-size: 2.2rem;
font-weight: 700;
text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}


.header p {


margin: 0;
opacity: 0.9;
font-size: 1.1rem;
}


.calculator-form {
padding: 2rem;
}


.form-row {
display: grid;
grid-template-columns: 1fr 1fr;
gap: 1.5rem;
margin-bottom: 1.5rem;
}


.form-group {
display: flex;
flex-direction: column;
}


.form-group.full-width {
grid-column: 1 / -1;
}


label {


font-weight: 600;
color: #2c3e50;
margin-bottom: 0.5rem;
font-size: 0.95rem;
}


small {
font-size: 0.8rem;
color: #7f8c8d;
margin-top: 0.25rem;
}


.select-input, .number-input {
padding: 0.875rem 1rem;
border: 2px solid #e1e8ed;
border-radius: 10px;
font-size: 1rem;
transition: all 0.3s ease;
background: white;
}


.select-input:focus, .number-input:focus {
outline: none;
border-color: #ffd700;
box-shadow: 0 0 0 3px rgba(255, 215, 0, 0.1);
transform: translateY(-2px);


}


.calculate-btn {
width: 100%;
padding: 1.2rem;
background: linear-gradient(135deg, #ffd700 0%, #ffb347 100%);
color: #2c3e50;
border: none;
border-radius: 12px;
font-size: 1.2rem;
font-weight: 700;
cursor: pointer;
transition: all 0.3s ease;
margin-top: 1rem;
display: flex;
align-items: center;
justify-content: center;
gap: 0.5rem;
text-transform: uppercase;
letter-spacing: 1px;
}


.calculate-btn:hover {
transform: translateY(-3px);
box-shadow: 0 10px 25px rgba(255, 215, 0, 0.3);
}


.btn-icon {
font-size: 1.5rem;
}


.result-card {
background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
margin: 0 2rem 2rem 2rem;
border-radius: 15px;
overflow: hidden;
animation: slideIn 0.5s ease-out;
}


@keyframes slideIn {
from {
opacity: 0;
transform: translateY(20px);
}
to {
opacity: 1;
transform: translateY(0);
}
}


.result-header {
background: linear-gradient(135deg, #28a745 0%, #20c997 100%);


padding: 1.5rem;
text-align: center;
}


.result-header h2 {
margin: 0;
color: white;
font-size: 1.5rem;
font-weight: 700;
}


.result-breakdown {
padding: 1.5rem;
}


.result-item {
display: flex;
justify-content: space-between;
align-items: center;
padding: 0.75rem 0;
border-bottom: 1px solid #dee2e6;
}


.result-item:last-child {
border-bottom: none;
}


.result-item.total {
background: linear-gradient(135deg, #ffd700 0%, #ffb347 100%);
margin: 1rem -1.5rem -1.5rem -1.5rem;
padding: 1.5rem;
color: #2c3e50;
font-weight: 700;
font-size: 1.2rem;
border-radius: 0 0 15px 15px;
}


.label {
font-weight: 600;
color: #495057;
}


.value {
font-weight: 700;
color: #2c3e50;
}


@media (max-width: 768px) {
.calculator-wrapper {
padding: 1rem;
}


.calculator-container {
margin: 0;
}


.header {
padding: 1.5rem;
}


.header h1 {
font-size: 1.8rem;
}


.calculator-form {
padding: 1.5rem;
}


.form-row {
grid-template-columns: 1fr;
gap: 1rem;
}


.result-card {
margin: 0 1.5rem 1.5rem 1.5rem;
}
}
</style>