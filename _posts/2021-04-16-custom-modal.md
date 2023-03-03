---
title: Build A Modal From Scratch
categories: [JavaScript]
layout: post
excerpt: "While redoing an earlier version of my website, again 😅, I decided it would be only HTML, CSS and JavaScript."
---

Hola. 👋🏾

While redoing an earlier version of my website, again 😅, I decided it would be only HTML, CSS and JavaScript. Below is an example of how I made a modal, using just those 3 technologies. (Not including media queries for responsiveness)

You can also view the repo with a gif of the code in action, [here](https://github.com/alishaevn/modal-from-scratch).

`index.html`
```js
<!DOCTYPE html>
<html lang='en'>

<head>
	<meta charset='UTF-8'>
	<meta name='viewport' content='width=device-width, initial-scale=1'>
	<title>Build A Modal From Scratch</title>
	<link href='index.css' rel='stylesheet' type='text/css'>
</head>

<body>
	<main class='container'>
		<h1>Click the image below</h1>
		<section id='projects'>
			<div class='blackout'></div>
			<img class='project-button' src='./assets/safer.png' alt='safeR web app' data-project-button='safer'>
			<aside class='popup-modal safer' data-project-modal='safer'>
				<div class='popup-modal__close'>
					Close
				</div>
				<div class='modal-mock-up safer'></div>
				<div class='app-details'>
					<h2 class='app-name safer'>safeR</h2>
				</div>
				<p class='app-blurb'>
					safeR is a React app with a React Native
					companion, complete with geolocation, that
					allows users to anonymously report local
					incidents.
				</p>
			</aside>
		</section>
	</main>
</body>
<script src='index.js'></script>

</html>
```

`index.css`
```js
/********
DEFAULT MOBILE STYLING
********/
* {
	margin: 0;
	padding: 0;
}

*,
*:before,
*:after {
	box-sizing: inherit;
}

a {
	text-decoration: none;
	color: inherit;
}

.app-blurb {
	font-size: 14px;
	text-align: center;
	margin: 20px auto;
	width: 300px;
}

.app-details {
	display: flex;
	margin: 15px auto;
	align-items: center;
	justify-content: center;
}

.app-name {
	font-size: 30px;
	font-weight: 100;
	letter-spacing: 1px;
	margin-left: 10px;
}

.blackout {
	position: absolute;
	z-index: 1010;
	left: 0px;
	width: 100%;
	height: 100%;
	background-color: rgba(0, 0, 0, 0.65);
	display: none;
}

body.hidden {
	overflow: hidden;
}

.container {
	padding-top: 35vh;
	display: flex;
	flex-direction: column;
	align-items: center;
}

html {
	box-sizing: border-box;
}

.modal-mock-up {
	background-size: cover;
	background-repeat: no-repeat;
	width: 330px;
	height: 300px;
	margin: 0 auto;
}

.popup-modal {
	height: 100%;
	width: 100%;
	position: absolute;
	left: 0px;
	padding: 20px;
	display: none;
	-webkit-transition: all 300ms ease-in-out;
	transition: all 300ms ease-in-out;
	z-index: 1011;
}

.popup-modal.is--visible {
	pointer-events: auto;
	display: initial;
}

.popup-modal__close {
	font-size: 20px;
	text-align: center;
	margin-left: 350px;
	cursor: pointer;
}

.project-button {
	display: inline-block;
	width: 300px;
	margin: 20px auto;
}

.proof {
	height: 20px;
	width: 20px;
	margin-right: 10px;
}

.proof-wrapper {
	justify-content: center;
	display: flex;
	bottom: 40px;
	position: absolute;
	margin-left: auto;
	margin-right: auto;
	left: 0;
	right: 0;
}

```

`index.js`
```js
'use strict'

const height = window.innerHeight
const width = window.innerWidth

const dividers = document.querySelectorAll('.divider')
const sections = document.querySelectorAll('section')

dividers.forEach(divider => divider.style.setProperty('--divider-width', width))
sections.forEach(section => {
	section.style.setProperty('--section-height', height)
	section.style.setProperty('--section-width', width)
})


// projects
const blackout = document.querySelector('.blackout')
const body = document.querySelector('body')
const modalOpenTriggers = document.querySelectorAll('.project-button')

modalOpenTriggers.forEach(trigger => {
	trigger.addEventListener('click', () => {
		const { projectButton } = trigger.dataset
		const popupModal = document.querySelector(`[data-project-modal='${projectButton}']`)

		setModalStyle(projectButton)
		addClasses(popupModal)

		popupModal.scrollIntoView()

		popupModal.querySelector('.popup-modal__close').addEventListener('click', () => removeClasses(popupModal))
		blackout.addEventListener('click', () => removeClasses(popupModal))
	})
})

const setModalStyle = project => {
	const modalBgImages = document.getElementsByClassName('modal-mock-up')
	const modalBgImage = [...modalBgImages].find(image => image.classList.contains(`${project}`))
	const appNames = document.getElementsByClassName('app-name')
	const appName = [...appNames].find(name => name.classList.contains(`${project}`))
	const modalBgColors = document.getElementsByClassName('popup-modal')
	const modalBgColor = [...modalBgColors].find(color => color.classList.contains(`${project}`))

	let image
	let name
	let color

	switch(project) {
		case 'safer':
			image = 'url(assets/safer-modal.png)'
			color = '#7BC087'
	}

	modalBgImage.style['background-image'] = image
	appName.style.color = name
	modalBgColor.style['background-color'] = color
}


const addClasses = modal => {
	modal.classList.add('is--visible')
	blackout.classList.add('is-blacked-out')
	body.classList.add('hidden')
}

const removeClasses = modal => {
	modal.classList.remove('is--visible')
	blackout.classList.remove('is-blacked-out')
	body.classList.remove('hidden')
}
```

See you next time. 🙃
