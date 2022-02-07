<template>
  <main id="app" @mousemove="mouseMove">
    <section class="products">
      <Product
        v-for="product in products"
        :key="product.color"
        :product="product"
      />
    </section>
  </main>
</template>

<script>
import Product from './components/Product';

export default {
  name: 'app',
  components: {
    Product
  },
  data () {
    return {
      products: [
        {
          title: 'Nike React Vision',
          color: 'green',
          bgtext: 'NIKE',
          src: require('./assets/green-shoe.png'),
          descriptie:'De Nike React Vision is een verhaal van buitengewoon comfort. Gelaagde texturen, vormen en levendige kleuren vormen samen een design dat is beïnvloed door de overdreven wereld van onze dromen. Het React foam en de ultrazachte tong bieden surrealistisch comfort.'
        },
        {
          title: 'Nike VaporMax',
          color: 'blue',
          bgtext: 'NIKE',
          src: require('./assets/blue-shoe.png'),
          descriptie:'De Nike Air VaporMax 2021 FK is gemaakt van minstens 40% gerecyclede materialen qua gewicht, en is luchtig en gemakkelijk te dragen dankzij het superelastische, gerecyclede Flyknit materiaal (en een zachte kraag die je enkel aanzet).Als je over straat loopt voelt het alsof je zweeft dankzij ongelooflijk zachte VaporMax demping.'
        },
        {
          title: 'Nike MD Runner 2',
          color: 'pink',
          bgtext: 'NIKE',
          src: require('./assets/pink-shoe.png'),
          descriptie: 'Knipoog naar de hardloopkampioen uit de jaren 90. De Nike MD Runner 2 behoudt de originele details met ventilerende mesh en details van zacht leer. Het low top design heeft een klassiek wafelpatroon en foam demping voor comfort.'
        }
      ]
    }
  },
  methods: {
    mouseMove (e) {
      let mouseX = e.clientX;
      let mouseY = e.clientY;

      let products = document.querySelectorAll('.products .product');

      for (let i = 0; i < products.length; i++) {
        let product = products[i];

        let product_image = product.querySelector('.product-image-wrap');

        let img_x = mouseX - this.coords(product_image).x;
        let img_y = mouseY - this.coords(product_image).y;
        product_image.style.transform = `translateY(-${img_y/40}px) translateX(-${img_x/40}px) translateZ(100px)`;

        let bgtext = product.querySelector('.bg-text');
        let bg_x = mouseX - this.coords(bgtext).x;
        bgtext.style.transform = `translateX(${bg_x/25}px)`;
      }
    },
    coords (el) {
      let coords = el.getBoundingClientRect();

      return {
        x: coords.left / 2,
        y: coords.top / 2
      }
    }
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    font-family: 'montseratt', sans-serif;
  }

  main {
    width: 100vw;
    min-height: 100vh;
    overflow: hidden;

    background-color: #EEE;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .products {
    display: flex;
    max-width: 1280px;
    padding: 25px;
    margin: 0 auto;
  }
</style>