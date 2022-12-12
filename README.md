# firebase-auth
MIT xPro Week 26 video 26.7

The next step is to set up email and password authentication for your application. Start by referencing Firebase and the Firebase authentication library within your login.html file, then add some code for the login page UI. Next, create a login.js file and configure the authentication process for the login page.

Finally, create a user and password, then log in to verify that authentication is working.

1. Set up Authentication with simple email/password enabled in your firebase project.

2. Add the firbase libraries, UI elements for inputs and buttons and the .js script reference to the html.

```
<!DOCTYPE html>
<html>
<head>
    <!-- The core Firebase JS SDK is always required and must be listed first -->
    <script src="https://www.gstatic.com/firebasejs/7.24.0/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/7.24.0/firebase-auth.js"></script>    
</head>

<input id="email" type="email" placeholder="Email"><br>
<input id="password" type="password" placeholder="Password"><br><br>
<button id="login">Login</button>
<button id="signup">SignUp</button>
<button id="logout" style="display:none;">Logout</button>

<script src="login.js"></script>

</html>
```

3. Create the firebase function

```
(function(){

}());
```

- Define the Web App's configuration object. This is provided in the firbase project settings. An example of the object is shown in step 1 above.

- Initialize Firebase

- Add the storage feature. Create a root reference.

- get UI elements by id

- enter code to upload a file to storage.

- enter code to download a file from storage.

```
(function(){

    // Your web app's Firebase configuration
    // For Firebase JS SDK v7.20.0 and later, measurementId is optional
    var firebaseConfig = {
        apiKey: "AIzaSyBboZP3WoD5Os9mOv4QGWej9Cu5lmI-bIM",
        authDomain: "course-92aae.firebaseapp.com",
        databaseURL: "https://course-92aae.firebaseio.com",
        projectId: "course-92aae",
        storageBucket: "course-92aae.appspot.com",
        messagingSenderId: "906967504618",
        appId: "1:906967504618:web:a5b51551a229502dc7a993",
        measurementId: "G-PWBBC8GN6B"
    };
    // Initialize Firebase
    firebase.initializeApp(firebaseConfig);

	// get elements
	const email    = document.getElementById('email');
	const password = document.getElementById('password');
	const login    = document.getElementById('login');
	const signup   = document.getElementById('signup');
	const logout   = document.getElementById('logout');

	// login
	login.addEventListener('click', e => {
		const auth  = firebase.auth();		
		const promise = auth.signInWithEmailAndPassword(email.value, password.value);
		promise.catch(e => console.log(e.message));
	});

	// signup
	signup.addEventListener('click', e => {
		// TODO: check for real email
		const auth  = firebase.auth();
		const promise = auth.createUserWithEmailAndPassword(email.value,password.value);
		promise.catch(e => console.log(e.message));
	});

    // logout
	logout.addEventListener('click', e => {
		firebase.auth().signOut();
	});

    // login state
	firebase.auth().onAuthStateChanged(firebaseUser => {
		if(firebaseUser){
			console.log(firebaseUser);
			logout.style.display = 'inline';
			login.style.display  = 'none';
			signup.style.display = 'none';
		}
		else{
			console.log('User is not logged in');
			logout.style.display = 'none';			
			login.style.display  = 'inline';
			signup.style.display = 'inline';
		}
	});

}());
```

4. Drag the html to the browser and upload an image file. Check the firebase project 