<script>
	let navOpen = false;
  
	function handleNav() {
	  navOpen = !navOpen;
	}
  
	function handleNavWithKey(e) {
	  if (e.code === "F1") {
		navOpen = !navOpen;
	  }
	}
  </script>
  
  <div id="mySidenav" class="sidenav" class:open={navOpen}>
	<a href="#a" class="closebtn" on:click={handleNav}>&times;</a>
	<a href="/src/index.html">Home</a>
	<a href="/src/Statistics/stat.svelte">Statistics</a>
	<div class="contacts">
		<p>Contacts: </p>
		<a href="mailto:valentinatruppia@gmail.com">Valentinatruppia@gmail.com</a>
		<a href="tel:+393665439236">3665439236</a>
	</div>

  </div>
  
  <div class="container" class:change={navOpen} on:click={handleNav}>
	<div class="bar1"></div>
	<div class="bar2"></div>
	<div class="bar3"></div>
  </div>
  
  <div id="main" class:pushMainToRight={navOpen}>
	<h2> </h2>
  </div>
  
  <svelte:window on:keydown={handleNavWithKey} />

	<style>
	.container {
		position: absolute;
		right: 10%;
	  display: inline-block;
	  cursor: pointer;
	}
	
	.bar1, .bar2, .bar3 {
	  width: 35px;
	  height: 5px;
	  background-color: #333;
	  margin: 6px 0;
	  transition: 0.4s;
	}
	
	.change .bar1 {
	  -webkit-transform: rotate(-45deg) translate(-9px, 6px);
	  transform: rotate(-45deg) translate(-9px, 6px);
	}
	
	.change .bar2 {opacity: 0;}
	
	.change .bar3 {
	  -webkit-transform: rotate(45deg) translate(-8px, -8px);
	  transform: rotate(45deg) translate(-8px, -8px);
	}
		
	/* The side navigation menu */
	.sidenav {
	  height: 100%; 
	  width: 0; /* 0 width - change this with JavaScript */
	  position: fixed;
	  z-index: 1;
	  top: 0;
	  left: 0;
	  background-color: #111; 
	  overflow-x: hidden; /* Disable horizontal scroll */
	  padding-top: 60px;
	  transition: 0.5s;
	}
	
	/* The navigation menu links */
	.sidenav a {
	  padding: 8px 8px 8px 32px;
	  text-decoration: none;
	  font-size: 25px;
	  color: #818181;
	  display: block;
	  transition: 0.3s;
	}
	.sidenav p {
	  padding: 450px 8px 8px 32px;
	  text-decoration: none;
	  font-size: 25px;
	  color: #818181;
	  display: block;
	  transition: 0.3s;
	}
	.sidenav .contacts a{
	  padding: 2px 8px 8px 32px;
	  text-decoration: none;
	  font-size: 15px;
	  color: #0000FF;
	  display: block;
	  transition: 0.3s;
	}
	
	/* When you mouse over the navigation links, change their color */
	.sidenav a:hover {
	  color: #f1f1f1;
	}
	
	/* Position and style the close button (top right corner) */
	.sidenav .closebtn {
	  position: absolute;
	  top: 0;
	  right: 25px;
	  font-size: 36px;
	  margin-left: 50px;
	}
	
	/* Style page content - use this if you want to push the page content to the right when you open the side navigation */
	#main {
	  transition: all .5s;
	  padding: 20px;
	}
		
	.pushMainToRight {
		margin-left: 40%
	/* 	transform: translate3d(40%, 0, 0); */
		
	}	
		
	.open {
		width: 40%;
	}	
	
	/* On smaller screens, where height is less than 450px, change the style of the sidenav (less padding and a smaller font size) */
	@media screen and (max-height: 450px) {
	  .sidenav {padding-top: 15px;}
	  .sidenav a {font-size: 18px;}
	}
	</style>