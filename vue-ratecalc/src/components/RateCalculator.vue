<template>
    <div>
      <h2>Räntekalkylatorn</h2>
      <label for="amount">Belopp:</label>
      <input type="number" v-model="amount" id="amount">
  
      <label for="interestRate">Ränta:</label>
      <input type="number" v-model="interestRate" id="interestRate">
  
      <label for="months">Månader:</label>
      <input type="number" v-model="months" id="months">
  
      <button @click="calculateTotal">Kalkylera</button>
  
      <p>Total: {{ total }}</p>
  
      <div>
        <canvas id="myChart"></canvas>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import Chart from 'chart.js/auto';
  
  const amount = ref(0);
  const interestRate = ref(0);
  const months = ref(0);
  const total = ref(0);
  const interest = ref(0);
  let myChart = null;
  
  const calculateTotal = () => {
    const principal = amount.value;
    const interestRateDecimal = interestRate.value / 100;
    const n = 12; 
    const t = months.value / 12;
  
    total.value = principal * Math.pow(1 + interestRateDecimal / n, n * t);
    interest.value = total.value - principal;
  
    updateChart();
  };
  
  const updateChart = () => {
    if (myChart) {
      myChart.data.labels = ['Total', 'Interest'];
      myChart.data.datasets[0].data = [total.value, interest.value];
      myChart.update();
    } else {
      myChart = new Chart(document.getElementById('myChart'), {
        type: 'bar',
        data: {
          labels: ['Total', 'Ränta'],
          datasets: [{
            label: 'Total och ränta',
            data: [total.value, interest.value],
            backgroundColor: ['#36a2eb', '#ff6384'],
          }],
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
        },
      });
    }
  };
  
  onMounted(() => {
    updateChart();
  });
  
  </script>
  
  <style scoped>
  h2 {
    color: #2c3e50;
    margin-bottom: 20px;
  }  

  input {
    margin-bottom: 10px;
    padding: 8px;
  }

  button {
    background-color: #3498db;
    color: #fff;
    padding: 10px 15px;
    border: none;
    cursor: pointer;
  }

  p {
    font-size: 18px;
    margin-top: 20px;
  }
</style>

  