<template>
	<div class="container fadeIn">
		<div class="wrapper">
			<Navbar />

			<!-- <div class="container"> -->
			<!-- Works list -->
			<div
				v-if="$route.path === '/'"
				:style="{
					marginTop: '14vw',
				}"
			>
				<Content />
			</div>

			<!-- Single project view -->
			<div class="single-project" v-if="isSingleProject">
				<SingleProjectHeader
					:title="$page.frontmatter.title"
					:year="$page.frontmatter.year.toString()"
					:categories="$page.frontmatter.categories"
				/>
				<Content />
			</div>

			<!-- Journal list -->
			<div v-if="$route.path === '/journal/'" class="journal-list">
				<Content />
			</div>

			<!-- Single journal -->
			<div v-if="isSingleJournal" class="single-journal">
				<Content />
			</div>
		</div>

		<Footer />
	</div>
</template>

<script>
export default {
	computed: {
		isSingleProject() {
			const worksRoute = "/works/";
			const path = this.$route.path;
			if (path.includes("works") && path.length >= worksRoute.length + 1) {
				return true;
			}
		},
		isSingleJournal() {
			const journalRoute = "/journal/";
			const path = this.$route.path;
			if (path.includes("journal") && path.length >= journalRoute.length + 1) {
				return true;
			}
		},
	},
	updated() {
		// unwrap all images from paragraph tags so we can have
		// different widths inside the content.

		document.querySelectorAll("p img").forEach((image) => {
			var wrapper = image.parentNode;
			let children = wrapper.children;
			let fragment = document.createDocumentFragment();

			Array.from(children).forEach((child) => {
				fragment.appendChild(child);
			});

			wrapper.parentNode.replaceChild(fragment, wrapper);
		});
	},
};
</script>

<style>
:root {
	--color-black: #1c1c1c;
	--text-black: #333333;
	--color-highlight: rgba(249, 233, 172, 0.99);
	--background: #ffffff; /*#FEF3E8;*/
	--background2: #ffffff;
}

/* @media (prefers-color-scheme: dark) {
	:root {
		--background: #111111; /*#333333; old color
		--background2: #111111; /*#333333; old color
		--color-black: #ffffff;
		--text-black: #ffffff;
	}
} */

* {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}

*::-moz-selection {
	background: var(--color-highlight);
	color: var(--color-black);
}

*::-webkit-selection {
	background: var(--color-highlight);
	color: var(--color-black);
}

*::selection {
	background: var(--color-highlight);
	color: var(--color-black);
}

body {
	font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Noto Sans",
		"Ubuntu", "Droid Sans", "Helvetica Neue", sans-serif;
	font-size: 1.25rem;
	background: var(--background);
	color: var(--color-black);
}

img {
	width: 100%;
	max-width: 100%;
	line-height: 0;
	margin: 2rem 0;
}

video {
	width: 100%;
	max-width: 100%;
	line-height: 0;
	/* margin: .5rem 0; */
	margin: 2rem 0;
}

.container {
	/* padding: 0 5vw; */
	/* max-width: 80vw; 60rem; */
	max-width: 75vw;
	margin: 0 auto;
}

.fadeIn {
	opacity: 1;
	animation: fadeIn ease-in 1.5s;
	/* animation-iteration-count: 1; */
	animation-timing-function: ease-in;
	/* animation-duration: 2s; */
}
@keyframes fadeIn {
	0% {
		opacity: 0;
	}
	100% {
		opacity: 1;
	}
}

@-moz-keyframes fadeIn {
	0% {
		opacity: 0;
	}
	100% {
		opacity: 1;
	}
}

@-webkit-keyframes fadeIn {
	0% {
		opacity: 0;
	}
	100% {
		opacity: 1;
	}
}

@-o-keyframes fadeIn {
	0% {
		opacity: 0;
	}
	100% {
		opacity: 1;
	}
}

@-ms-keyframes fadeIn {
	0% {
		opacity: 0;
	}
	100% {
		opacity: 1;
	}
}

.journal-list,
.single-journal {
	width: 800px;
	max-width: 100%;
	margin: 0 auto;
}

h1,
h2 {
	font-family: "EB Garamond";
	font-weight: bold;
	letter-spacing: -0.03em;
}

h1,
h2,
h3,
h4,
h5,
h6,
p {
	width: 100%;
	/* max-width: 800px; */
}

/* @media screen and (max-width: 600px) {
	h1,
	h2,
	h3,
	h4,
	h5,
	h6,
	p {
		width: 100%;
	}
} */

h1 {
	font-size: 6rem;
	line-height: 1.15;
	/* margin: 0 auto 3rem auto; */
	margin: 3rem 0;
	/* font-family: 'Abril Fatface',  -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Noto Sans", "Ubuntu", "Droid Sans", "Helvetica Neue", sans-serif; */
}

h2 {
	font-size: 2rem;
	font-weight: 500;
	/* margin: 2rem auto 2rem auto; */
	margin: 6rem 0;
	/* font-family: 'Abril Fatface', -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Noto Sans", "Ubuntu", "Droid Sans", "Helvetica Neue", sans-serif; */
}

h3 {
	font-size: 1rem;
	font-weight: 700;
	/* margin: 2rem auto 1rem auto; */
	margin: 1rem 0;
}

h4 {
	font-size: 0.8rem;
	font-weight: 700;
	/* margin: 2rem auto 1rem auto; */
	margin: 1rem 0;
}

p {
	font-family: "Circular Std";
	font-size: 1.25rem;
	line-height: 1.6;
	/* margin: 1rem auto 2rem auto; */
	margin-bottom: 2rem;
	/* font-family: "CircularStd";
    font-weight: normal;
    font-style: normal; */
	color: var(--text-black);
}

pre {
	background: var(--color-black);
	padding: 1rem;
	margin: 1rem 0;
}

code {
	color: white;
	background: var(--color-black);
	font-size: 0.8rem;
	padding: 0.05rem 0.25rem;
	font-weight: 400;
}

.single-project {
	/* padding: 5vw; */
	/* padding: 0 5vw; */
}

hr {
	content: "";
	display: block;
	color: #595959;
	max-width: 100%;
	margin: 4rem auto;
	overflow: hidden;
	margin: 2rem 0;

	/* from daniel eden portfo */
	border: 2px solid;
	border-radius: 2px;
	unicode-bidi: isolate;
	/* margin-block-start: 0.5em;
	margin-block-end: 0.5em; */
	margin-inline-start: auto;
	margin-inline-end: auto;
}

.photoInfo {
	font-size: 0.8rem;
}

.workAtag {
	color: var(--color-black);
	margin: 3rem 0;
	cursor: pointer;
	/* border-bottom: 1px solid transparent; */
	transition-duration: 0.3s;
	transition-property: transform;
	transition-timing-function: ease-out;
}

.workAtag:hover {
	text-decoration: none;
	color: #fb0d1b;
	transition-duration: 0.3s;
	transition-property: transform;
	transition-timing-function: ease-out;
	transform: translateY(-2px);
}
</style>
