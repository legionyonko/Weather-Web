<template>
  <div class="state">
    <header>
      <h1>States</h1>
      <input type="text" placeholder="Search...">
    </header>
    <div class="options-container">
      <div class="card">
        <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAT4AAACfCAMAAABX0UX9AAAAjVBMVEX80RbaJR3////rjRrZFh391hbXAB7+2hXYAADaIRjdPjjZGAzYDQDZGxHaIBf76unwtrTfTUj++Pj1zs3ywL/qlJHgUk754uHcNS/leXbmf3z319bbKiLcMCn98/PvsK7tpKLiYl743dzzxsXoiof1z87jbGjuqafeRUDrmJXldXHhXFfnhYPhXlvsn5yJMbZwAAAE1UlEQVR4nO3c2ZqiOhiF4YK9d1UoAs5azuLQWt229395WyhRfhRFFjz6xPWd9EEPB28nkoSUb9ZT9/7x9tw9Guh65IMiHxT5oMgHRT6o1+DztVZKa8+NfnWdUv7RsBfg85RqdOrDWtPe16y16svP0vxM53O0+tWO4OJq7WUwKsXOMp3PUaP1JGnX+x7vJ69fEp7hfHpUT9rZ7Y3S5X3uhRnM56lvgVcfq/KG3SFz+VRXTNt5Q5U78KKM5UsNvU75Iy/MUD5HtZN4k64qly3OTD5HD8Xz1nFLZoszks9RvaTesJqJG2YknxJjb17FM+OQiXzyc69W8lJPZCCfXopn7riymWuZyOc1hN5vffuv+IXHp3l8qia2GjlWLH63UdTPOD4tlsvNPGd7erIh30/OSEzdQY6pq+p24QNA0/j0VDx1c0xd3bfJd8jxxODr395t+GObfHF6du/gizYo5DtgiMdu58In35fSyYWgWtvki/P+yBXzuYrfrc02J0E3sMl3TIvD+eGluRvuSWrrxo+g4zXJd0rO3e+Lqxa1CH9vMv2jtKdWNvmOOV9i7nYv7nYd93CIvxfs2OQ75faTes2MJXPqA5J8cXqXNJlnLVvULM33VfRUxig+edDXzlz1qXmKb6BUseN8s/gEyy5zvxvtNGSLvqcKXB0yi088eJfZA0r/PvOz7dbAuVvQLD7xYnxwZT6q+gU/215tfeW9Lp+wuHpeIAdqonn/Hj+z+MRNtGujzz1fvETVpn9fePSJIbXN5os3aym7dVeeJ7wan3g7fum8Jf6DrXO7WeNeO+P4xOvxeiZf6lWmbfd2mwJ2pvHJk/pV1rLZ36SH3qiQnXF8naRJ5lnz+VOXe94w/+ZpaaR3XPMNe+RLpsUD9fLCL95xrJZj9UW+ZPHx55Vnx89+t7V1ww2a7pMvkSseqZOLh/W9/eZWx5vbwxkN+aJSdwyC8x2EH4TjLqFZI98pOXsvnfj58gPR25AvoRHkefYmixY75Dsk923TPNcMVuQ75sqDUOu2S3h8QL44eWC/yDH83IB8x3x5NzfI8QpITXm79ISxFmu/PG8v3HEBuSjz+FJPj8xzl1IykM+XVzV2VfoZyGe5f4VfnvvNRTORL/0aN6hu/BnJZ6m+HH+V+ZnJZ2m5edtV9VOBhvJZuiFuHLTcan6i11Q+y9PiZeQkqGQAGstnOWorJvBiVAGguXz7CezLi0DT8X33f3JkMt9+AH5KwMUvXeQWX3ZG8+13IMrpiD1cs963dHlj0HC+8CK9+uysxAvMYb8MuSjj+azoW9SUH2y/Z9PprjNoaI6+u3PCrz4MK/Hr06zX4aso8kGRD4p8UOSDenq+f5+694//nrq3fxjQ26P//6738f7o8X+9R3923Ojj/dGfvtd7tM+NyAdFPijyQZEPinxQ5IMiHxT5oMgHRT4o8kGRD4p8UOSDIh8U+aDIB0U+KPJBkQ+KfFDkgyIfFPmgyAdFPijyQZEPinxQ5IMiHxT5oMgHRT4o8kGRD4p8UOSDIh8U+aDIB0U+KPJBkQ+KfFDkgyIfFPmgyAdFPijyQZEPinxQ5IMiHxT5oMgHRT4o8kGRD4p8UOSDIh8U+aDIB0U+KPJBkQ+KfFDkgyIfFPmgyAdFPijyQZEP6tn5/gcZbaOkAHr5WwAAAABJRU5ErkJggg==" alt="" >
        <div class="districts-cards">
          <h2>Selangor</h2>
          <p>9 districts</p>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>

  .container{
    max-width: 1000px;
    margin: 0 auto;

  }
  header{
    margin-bottom: 10px;
    margin-top: 30px;
    display: flex;
    align-items: center;
  }
  header h1{
    font-weight: bold;
    margin-right: 30px;
  }
  header input{
    border: none;
    background-color: rgb(255, 255, 255) ;
    padding: 10px;
    border-radius: 5px;
  }

  .options-container{
    display: flex;
    flex-wrap: wrap;
    margin-top: 40px;
  }

  .card{
    width: 290px;

    overflow: hidden;
    border-radius: 2%;
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
    margin-bottom: 35px;
    margin-right: 20px;
    cursor: pointer;
  }
  .card img{
    width: 100%;
    height: 190px;
    margin: 0;
  }
  .card .card-text{
    padding:  5 5px;
  }
  .card .card-text h2{
    font-weight:bold ;
  }
</style>