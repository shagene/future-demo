<script>
	import { goto } from '$app/navigation';
  </script>
  
  <div class="error-container">
	<h1>Oops! Something went wrong.</h1>
	<p>We're sorry for the inconvenience. Please try again later.</p>
	<button class="btn btn-rounded" on:click={() => goto('/')}>Back to Home</button>
  </div>
  
  <style>
	.error-container {
	  display: flex;
	  flex-direction: column;
	  justify-content: center;
	  align-items: center;
	  height: 100vh;
	  text-align: center;
	}
	h1 {
	  margin-bottom: 1rem;
	}
	p {
	  margin-bottom: 2rem;
	}
	.btn {
	  padding: 0.5rem 1rem;
	  font-size: 1rem;
	  cursor: pointer;
	  background-color: #93186c;
	  color: #FFF;
	  border: none;
	  border-radius: 25px;
	  transition: background-color 0.3s, opacity 0.3s, transform 0.1s;
	}
	.btn:hover {
	  background-color: #a52f80; /* A slightly lighter shade for hover */
	  opacity: 0.9;
	}
	.btn:active {
	  transform: scale(0.98); /* Slightly scale down the button when clicked */
	}
  </style>
  