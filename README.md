<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Factorial Calculator</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
  <style>
    /* Remove spinner arrows */
    input[type=number]::-webkit-outer-spin-button,
    input[type=number]::-webkit-inner-spin-button {
      -webkit-appearance: none;
      margin: 0;
    }
    input[type=number] {
      -moz-appearance: textfield;
    }
  </style>
</head>
<body class="bg-light p-5">

  <div class="container">
    <h2 class="text-center mb-4">🔢 Factorial Calculator</h2>

    <div class="row justify-content-center">
      <div class="col-md-6">

        <!-- Input field -->
        <input type="number" id="numberInput" class="form-control mb-3" placeholder="Enter a number" min="0">

        <!-- Toggle for method -->
        <div class="form-check form-switch mb-3">
          <input class="form-check-input" type="checkbox" id="methodToggle">
          <label class="form-check-label" for="methodToggle">Use Reduce Method</label>
        </div>

        <!-- Button -->
        <button class="btn btn-primary w-100" onclick="calculateFactorial()">Calculate Factorial</button>

        <!-- Result -->
        <div id="result" class="alert alert-info text-center mt-4" style="display: none;"></div>

      </div>
    </div>
  </div>

  <!-- Bootstrap JS -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

  <!-- JavaScript -->
  <script>
    function factorialForLoop(n) {
      if (n === 0 || n === 1) return 1;
      let result = 1;
      for (let i = 1; i <= n; i++) {
        result *= i;
      }
      return result;
    }

    function factorialReduce(n) {
      if (n === 0 || n === 1) return 1;
      return Array.from({ length: n }, (_, i) => i + 1)
                  .reduce((acc, val) => acc * val, 1);
    }

    function calculateFactorial() {
      const num = parseInt(document.getElementById("numberInput").value);
      const useReduce = document.getElementById("methodToggle").checked;
      const resultDiv = document.getElementById("result");

      if (isNaN(num) || num < 0) {
        resultDiv.style.display = "block";
        resultDiv.className = "alert alert-danger text-center mt-4";
        resultDiv.textContent = "Please enter a non-negative number.";
        return;
      }

      const result = useReduce ? factorialReduce(num) : factorialForLoop(num);
      const method = useReduce ? "Reduce Method" : "For Loop";

      resultDiv.style.display = "block";
      resultDiv.className = "alert alert-success text-center mt-4";
      resultDiv.textContent = `Factorial of ${num} using ${method} is ${result}`;
    }
  </script>

</body>
</html>
