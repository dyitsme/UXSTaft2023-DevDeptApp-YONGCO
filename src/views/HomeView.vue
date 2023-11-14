<script setup>
// import Navbar from '../components/Navbar.vue'
import Card from '../components/Card.vue'
// import Footer from '../components/Navbar.vue'
import { ref } from 'vue'
import Clipboard from 'clipboard'


const originalLink = ref('')
const links = ref([])


function shortenLink() {
  const url = `https://csclub.uwaterloo.ca/~phthakka/1pt-express/addURL?long=${originalLink.value}`
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
    links.value = [...links.value, {
      'long': data.long,
      'short': `https://1pt.co/${data.short}`
    }]
 })
  .catch(err => {
    console.error(err);
  })

}

function copyToClipboard(shortLink) {
  const clipboard = new Clipboard('.copy-btn', {
    text: function () {
      return shortLink;
    }
  });

  clipboard.on('success', function (e) {
    console.log('Copied to clipboard');
    e.clearSelection();
  });

  clipboard.on('error', function (e) {
    console.error('Unable to copy to clipboard');
  });

  clipboard.destroy();
}

function removeCard(itemId) {
  // links.value = links.value.filter(link => link.id !== itemId);
  console.log("hello")
  console.log(itemId)
}
</script>

<template>
    <input type="text" v-model="originalLink">
    <button @click="shortenLink">Shorten</button>
    <div v-for="link in links" :key="link.id">
      <Card :long="link.long" :short="link.short" @copy="copyToClipboard(link.short)" @remove="removeCard(link.id)"/>
    </div>
</template>
