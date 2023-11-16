<script setup>
import Navbar from '../components/Navbar.vue'
import Card from '../components/Card.vue'
import Footer from '../components/Footer.vue'
import { ref } from 'vue'
import Clipboard from 'clipboard'
import isUrlHttp from 'is-url-http'
import 'boxicons'


const originalLink = ref('')
const links = ref([])
const isNotValid = ref(false)


function shortenLink() {
  const url = `https://csclub.uwaterloo.ca/~phthakka/1pt-express/addURL?long=${originalLink.value}`
  // check if the url is valid
  if (isUrlHttp(originalLink.value)) {
    fetch(url, {
      method: 'POST',
      headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json',
      },
      // body: JSON.stringify(data)
    })
    .then(res => {
      return res.json()
    })
    .then(data => {
      console.log(data)
      links.value.push({
        'long': data.long,
        'short': `https://1pt.co/${data.short}`
      })

      // reset form
      originalLink.value = ''
      isNotValid.value = false
  })
    .catch(err => {
      console.error(err);
    })
  }
  else {
      isNotValid.value = true
  }


}

function copyToClipboard(short) {
    navigator.clipboard.writeText(short)
}

function removeCard(link) {
  links.value = links.value.filter((l) => l !== link)
}

</script>

<template>
    <Navbar/>
    <div class="intro">
      <div class="intro-text">
        <h2>Create a Short URL</h2>
        <p>Shorten your long links to make it easy on other people's eyes.</p>
      </div>
      <img src="../assets/img/man-working-on-laptop.svg">
    </div>
    <div class="input-group">
      <input class="input-link" type="text" v-model="originalLink" placeholder="Paste a link here...">
      <button class="shorten-btn" @click="shortenLink">Shorten</button>
    </div>
    <div class="not-valid" v-if="isNotValid">Invalid url or no url provided</div>
    <div v-for="(link, index) in links" :key="index">
      <Card :long="link.long" :short="link.short" @copy="copyToClipboard(link.short)" @remove="removeCard(link)"/>
    </div>
    <Footer/>
</template>

<style scoped>
@import '../assets/main.css';
.intro {
  display: flex;
  color: var(--black);
  padding: 2rem 10rem;
}
h2 {
  font-size: 4rem;
}
p {
  font-size: 1.5rem;
}
img {
  display: block;
  margin-left: auto;
  margin-right: auto;
  max-width: 428px;
  max-height: 428px;
}


.input-group {
  display: flex;
  justify-content: center;
}
.input-link {
  font-size: 1.5rem;
  border-radius: 10px;
  border: 2px solid var(--grey);
  min-width: 960px;
  margin-right: 20px;
  padding-left: 20px;
  padding-right: 0px;
}
.shorten-btn {
  background-color: var(--primary-green);
  color: var(--white);
  border: none;
  border-radius: 10px;
  min-height: 71px;
  min-width: 210px;
  font-size: 1.5rem;
  cursor: pointer;
}

.shorten-btn:hover {
  background-color: var(--active-green);
  color: var(--white);
  transition: 0.25s;
}
.shorten-btn:active {

  background-color: #34D399;
  background-size: 100%;
  transition: background 0s;
}

.not-valid {
  display: flex;
  color: var(--red);
  font-size: 1.5rem;
  justify-content: center;
}
</style>
