<template>
  <div class="hello">
    <div class="row" style="padding-right: 120px; padding-left: 120px">
      <div class="col-6 mx-auto" style="margin-top: 40px">
        <nav
          class="navbar navbar-light bg-light"
          style="background-color: transparent !important"
        >
          <router-link to="/" class="navbar-brand">
            <img
              src="../assets/images/klasha-logo.png"
              alt="Klasha logo"
              style="width: 40px; height: 40px"
            />
            <span style="margin-left: 12px; font-weight: 500">Store</span>
          </router-link>
          <span
            data-toggle="dropdown"
            aria-haspopup="true"
            aria-expanded="false"
            style="cursor: pointer"
          >
            <img
              src="../assets/images/shopping-cart.svg"
              alt="Shopping Cart"
              style="width: 20px; height: 20px; font-weight: 400; font-size: 20"
            />
            Cart
            <span
              style="
                width: 22px;
                height: 22px;
                background-color: #ef2c5a;
                display: inline-block;
                border-radius: 22px;
                color: white;
                text-align: center;
                margin-left: 8px;
              "
              >{{ cartSize }}</span
            >
          </span>
          <div
            class="dropdown-menu dropdown-menu-right"
            style="width: 440px; padding: 20px"
          >
            <!-- nskdjsdj -->
            <div v-for="item in cart" :key="item.name" class="row p-1">
              <div class="col-8">
                <div class="row">
                  <img
                    class="col-3 pr-0"
                    :src="require(`@/assets/images/${item.image}`)"
                    style="object-fit: contain"
                    alt=""
                  />
                  <span class="col-9">
                    <p class="mb-0" style="font-weight: 500; font-size: 18px">
                      {{ item.name }}
                    </p>
                    <p
                      class="mb-0"
                      style="font-weight: 400; color: #81818a; font-size: 10px"
                    >
                      {{ item.shipping }}
                    </p>
                  </span>
                </div>
              </div>

              <div class="col-4">
                <p style="font-weight: 700; font-size: 16px; float: right">
                  ₦
                  {{
                    new Intl.NumberFormat('en-US', {
                      minimumFractionDigits: 2,
                    }).format(item.price)
                  }}
                </p>
              </div>
            </div>

            <router-link
              to="/checkout"
              v-if="cartSize > 0"
              @click="addTotalPrice2(item.price)"
              class="text-center text-white pt-2 pb-2"
              type="button"
              style="
                border: none;
                display: block;
                width: 100%;
                margin: auto;
                margin-top: 40px;
                background: #ef2c5a;
                text-decoration: none;
              "
            >
              Proceed to checkout
            </router-link>

            <div
              v-if="cartSize == 0"
              class="text-center text-white pt-2 pb-2"
              type="button"
              style="
                border: none;
                display: block;
                width: 100%;
                margin: auto;
                margin-top: 40px;
                background: #ef2c5a;
                text-decoration: none;
                cursor: not-allowed;
              "
            >
              Empty
            </div>
          </div>
        </nav>
      </div>
    </div>
    <h3
      class="text-center"
      style="font-weight: 800; font-size: 64px; margin-top: 143px"
    >
      Nike Collections
    </h3>
    <!-- <helss -->
    <div class="container">
      <div class="row">
        <div
          v-for="product in products"
          :key="product.name"
          class="col-3"
          style="padding: 16px"
        >
          <img
            :src="require(`../assets/images/${product.image}`)"
            alt="boot"
            class="img-fluid"
          />
          <div style="margin-top: 12px">
            <p style="font-weight: 400; font-size: 16px; color: #686873">
              {{ product.name }}
            </p>
            <p style="font-weight: 700; font-size: 24px; margin-top: 12px">
              ₦
              {{
                new Intl.NumberFormat('en-US', {
                  minimumFractionDigits: 2,
                }).format(product.price)
              }}
            </p>
            <p
              style="
                font-weight: 400;
                font-size: 14px;
                margin-top: 12px;
                color: #686873;
              "
            >
              {{ product.shipping }}
            </p>
          </div>
          <div class="row">
            <div class="col-6 d-flex" style="color: #fb8200; font-size: 10px">
              <span class="justify-content-center align-self-center">
                <span class="fa fa-star checked"></span>
                <span class="fa fa-star checked"></span>
                <span class="fa fa-star checked"></span>
                <span class="fa fa-star checked"></span>
                <span class="fa fa-star-o"></span>
                <span
                  style="
                    margin-left: 10px;
                    font-weight: 500;
                    color: #4f4f5b;
                    font-size: 14px;
                  "
                  >{{ product.rating }}</span
                >
              </span>
            </div>
            <div class="col-6">
              <button
                style="
                  background: #ef2c5a;
                  color: white;
                  padding: 6px;
                  border: none;
                "
              >
                <img src="../assets/images/shopping-cart-white.svg" alt="" />
                <span
                  style="font-size: 12px; padding-left: 8px"
                  @click="addToCart(product)"
                  >Add to Cart</span
                >
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data() {
    return {
      products: [
        {
          name: 'Nike Mercurial Superfly 7 Elite Mbappé Rosa FG',
          price: 12000,
          shipping: 'Eligible for Shipping To Mars or somewhere else',
          rating: 4.05,
          image: 'nike-1.png',
        },
        {
          name: 'Nike Air VaporMax Plus',
          price: 10500,
          shipping: 'Eligible for Shipping To Mars or somewhere else',
          rating: 4.05,
          image: 'nike-2.png',
        },
        {
          name: 'Nike Air Max 270 G',
          price: 8000,
          shipping: 'Eligible for Shipping To Mars or somewhere else',
          rating: 4.05,
          image: 'nike-3.png',
        },
        {
          name: 'NikeCourt Air Zoom GP Turbo Naomi Osaka',
          price: 15000,
          shipping: 'Eligible for Shipping To Mars or somewhere else',
          rating: 4.05,
          image: 'nike-4.png',
        },
        {
          name: 'Nike Air Zoom Pegasus 38 Shield By You',
          price: 11500,
          shipping: 'Eligible for Shipping To Mars or somewhere else',
          rating: 4.05,
          image: 'nike-5.png',
        },
        {
          name: 'Nike Air Force 1 GTX Boot',
          price: 10000,
          shipping: 'Eligible for Shipping To Mars or somewhere else',
          rating: 4.05,
          image: 'nike-6.png',
        },
        {
          name: 'Nike Air Max Plus SE',
          price: 18000,
          shipping: 'Eligible for Shipping To Mars or somewhere else',
          rating: 4.05,
          image: 'nike-7.png',
        },
        {
          name: 'Nike Air Zoom Terra Kiger 7',
          price: 5000,
          shipping: 'Eligible for Shipping To Mars or somewhere else',
          rating: 4.05,
          image: 'nike-8.png',
        },
      ],
      cart: [],
      cartSize: 0,
      totalPrice: 0,
    };
  },
  methods: {
    addToCart(item) {
      this.cartSize++;
      this.cart.push(item);
      this.totalPrice += item.price;
      sessionStorage.setItem('price', this.totalPrice);
    },

    addTotalPrice() {
      this.cart.reduce(function (sum, current) {
        return sum + current.price;
      }, 0);
    },

    addTotalPrice2(input) {
      alert('jkhksddk');
      console.log('input', input);
      var total = 0;
      for (let i = 0; i <= this.cart.length; i++) {
        total += input[i];
      }
      console.log(total);
      sessionStorage.setItem('price', total);
      return total;
    },
  },
  beforeMount() {
    sessionStorage.clear();
  },
};
</script>
