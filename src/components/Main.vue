<!-- eslint-disable vue/multi-word-component-names -->
<script>
import '../styles/main.sass';

export default {
  name: 'MAIN',
  data: () => ({
    option: 'thumbnail one',
    popupValue: '',
    openPopup: false,
    counter: 0,
    total: 0,
    totalFormat: 0,
    counterPopup: 0,
    openCart: false,
    counterOptionMobile: 1,
    openCloseMenu: false,
  }),
  methods: {
    handleThumbnails: function (value) {
      this.option = value;
    },
    handleCounterMinus: function () {
      this.counter--;
      if (this.counter < 1) this.counter = 0;
      this.handleSubtractValue();
    },
    handleCounterPlus: function () {
      this.counter++;
      this.handleAddAmount();
    },
    handleOpenCart: function () {
      this.openCart = !this.openCart;
    },
    handleAddAmount: function () {
      const value = 125;
      this.total += value;
      const numberFormat = Intl.NumberFormat('en-US', {
        style: 'currency',
        currency: 'USD',
      }).format(this.total);
      this.totalFormat = numberFormat;
    },
    handleSubtractValue: function () {
      const value = 125;
      if (this.total > 0) {
        this.total -= value;
      } else {
        return;
      }
      const numberFormat = Intl.NumberFormat('en-US', {
        style: 'currency',
        currency: 'USD',
      }).format(this.total);
      this.totalFormat = numberFormat;
    },
    handleDeleteProductCart: function () {
      this.counter = 0;
      this.total = 0;
    },
    handlePopupPreviewProduct: function (opt, value) {
      this.openPopup = !this.openPopup;
      this.popupValue = opt;
      this.counterPopup = Number(value);
    },
    handleClosePopup: function () {
      this.openPopup = false;
    },
    handlePrevious: function () {
      if (this.counterPopup > 1) {
        this.counterPopup--;
      } else {
        return;
      }
      this.popupValue = String(this.counterPopup);
    },
    handleNext: function () {
      if (this.counterPopup < 4) {
        this.counterPopup++;
      } else {
        return;
      }

      this.popupValue = String(this.counterPopup);
    },
    handleNextMobileOption: function () {
      if (this.counterOptionMobile < 4) {
        this.counterOptionMobile++;
      }

      switch (this.counterOptionMobile) {
        case 1:
          this.option = 'thumbnail one';
          break;
        case 2:
          this.option = 'thumbnail two';
          break;
        case 3:
          this.option = 'thumbnail three';
          break;
        case 4:
          this.option = 'thumbnail four';
          break;
      }
    },
    handlePreviousMobileOption: function () {
      if (this.counterOptionMobile > 1) {
        this.counterOptionMobile--;
      }
      switch (this.counterOptionMobile) {
        case 1:
          this.option = 'thumbnail one';
          break;
        case 2:
          this.option = 'thumbnail two';
          break;
        case 3:
          this.option = 'thumbnail three';
          break;
        case 4:
          this.option = 'thumbnail four';
          break;
      }
    },
    handleOpenCloseMenu: function () {
      this.openCloseMenu = !this.openCloseMenu;
    },
  },
};
</script>

<template>
  <header class="header">
    <img
      src="../assets/icon-menu.svg"
      alt="icon menu"
      class="menu"
      @click="handleOpenCloseMenu"
    />
    <img src="../assets/logo.svg" alt="logo" class="logo" />
    <span :class="openCloseMenu ? 'background_open' : 'background'"></span>
    <ul :class="openCloseMenu ? 'list_open' : 'list'">
      <img
        src="../assets/icon-close.svg"
        alt="icon close"
        class="menu_close"
        @click="handleOpenCloseMenu"
      />
      <li>collections</li>
      <li>men</li>
      <li>women</li>
      <li>about</li>
      <li>contact</li>
    </ul>
    <span class="profile">
      <span :class="counter > 0 ? 'wrapper' : 'wrapper_hide'">
        {{ counter }}
      </span>
      <img src="../assets/icon-cart.svg" alt="icon cart" class="cart" />
      <img
        src="../assets/image-avatar.png"
        alt="image avatar profile"
        class="photo"
        @click="handleOpenCart"
      />
      <!-- shopping cart popupValue that shows the amount of products added to the cart -->
      <div :class="openCart ? 'popup_cart' : 'popup_cart_close'">
        <strong>cart</strong>
        <span class="wrapper_product" v-if="counter > 0">
          <img
            src="../assets/image-product-1-thumbnail.jpg"
            alt="thumbnail product"
            class="product_thumbnail"
          />
          <span class="info">
            <p>fall limited edition sneakers</p>
            <!-- <p>{{ counter }}</p> -->
            <p>
              $125.00 x {{ counter }}
              <strong class="total">{{ totalFormat }}</strong>
            </p>
          </span>
          <img
            src="../assets/icon-delete.svg"
            alt="icon trash"
            class="trash"
            @click="handleDeleteProductCart"
          />
        </span>
        <span class="wrapper_product_empty" v-else> your cart is empty </span>
        <button class="checkout" v-if="counter > 0">checkout</button>
      </div>
      <!-- final-->
    </span>
  </header>
  <main class="main">
    <!-- popupValue that previews the product in an expanded form -->
    <span :class="openPopup ? 'wrapper_img' : 'wrapper_img_close'">
      <span>
        <img
          src="../assets/icon-close.svg"
          alt="closer icon"
          class="close"
          @click="handleClosePopup"
        />
        <img
          src="../assets/icon-previous.svg"
          alt="previous"
          class="previous"
          @click="handlePrevious"
        />

        <img
          v-if="popupValue == 'thumbnail one' || popupValue == '1'"
          src="../assets/image-product-1.jpg"
          alt="image product"
          class="product1"
        />
        <img
          v-else-if="popupValue == 'thumbnail two' || popupValue == '2'"
          src="../assets/image-product-2.jpg"
          alt="image product"
          class="product1"
        />
        <img
          v-else-if="popupValue == 'thumbnail three' || popupValue == '3'"
          src="../assets/image-product-3.jpg"
          alt="image product"
          class="product1"
        />
        <img
          v-else-if="popupValue == 'thumbnail four' || popupValue == '4'"
          src="../assets/image-product-4.jpg"
          alt="image product"
          class="product1"
        />
        <img
          src="../assets/icon-next.svg"
          alt="next"
          class="next"
          @click="handleNext"
        />
      </span>

      <span class="thumbnailz">
        <span
          :class="
            popupValue == 'thumbnail one' || popupValue == '1'
              ? 'wrapper_active-border'
              : 'wrapper_popup'
          "
        >
          <img
            src="../assets/image-product-1-thumbnail.jpg"
            alt="thumbnail1"
            :class="
              popupValue == 'thumbnail one' || popupValue == '1'
                ? 'thumbnail_opaque'
                : 'thumbnail'
            "
          />
        </span>
        <span
          :class="
            popupValue == 'thumbnail two' || popupValue == '2'
              ? 'wrapper_active-border'
              : 'wrapper_popup'
          "
        >
          <img
            src="../assets/image-product-2-thumbnail.jpg"
            alt="thumbnail2"
            :class="
              popupValue == 'thumbnail two' || popupValue == '2'
                ? 'thumbnail_opaque'
                : 'thumbnail'
            "
          />
        </span>
        <span
          :class="
            popupValue == 'thumbnail three' || popupValue == '3'
              ? 'wrapper_active-border'
              : 'wrapper_popup'
          "
        >
          <img
            src="../assets/image-product-3-thumbnail.jpg"
            alt="thumbnail3"
            :class="
              popupValue == 'thumbnail three' || popupValue == '3'
                ? 'thumbnail_opaque'
                : 'thumbnail'
            "
          />
        </span>
        <span
          :class="
            popupValue == 'thumbnail four' || popupValue == '4'
              ? 'wrapper_active-border'
              : 'wrapper_popup'
          "
        >
          <img
            src="../assets/image-product-4-thumbnail.jpg"
            alt="thumbnail4"
            :class="
              popupValue == 'thumbnail four' || popupValue == '4'
                ? 'thumbnail_opaque'
                : 'thumbnail'
            "
          />
        </span>
      </span>
    </span>
    <!-- final -->

    <div class="images__container">
      <img
        src="../assets/icon-previous.svg"
        alt="previous"
        class="previous_container"
        @click="handlePreviousMobileOption"
      />
      <img
        v-if="option == 'thumbnail one'"
        src="../assets/image-product-1.jpg"
        alt="image product"
        class="product"
        @click="handlePopupPreviewProduct('thumbnail one', '1')"
      />
      <img
        v-else-if="option == 'thumbnail two'"
        src="../assets/image-product-2.jpg"
        alt="image product"
        class="product"
        @click="handlePopupPreviewProduct('thumbnail two', '2')"
      />
      <img
        v-else-if="option == 'thumbnail three'"
        src="../assets/image-product-3.jpg"
        alt="image product"
        class="product"
        @click="handlePopupPreviewProduct('thumbnail three', '3')"
      />
      <img
        v-else
        src="../assets/image-product-4.jpg"
        alt="image product"
        class="product"
        @click="handlePopupPreviewProduct('thumbnail four', '4')"
      />
      <img
        src="../assets/icon-next.svg"
        alt="next"
        class="next_container"
        @click="handleNextMobileOption"
      />

      <span class="thumbnails">
        <span
          :class="
            option == 'thumbnail one' ? 'wrapper_active-border' : 'wrapper'
          "
        >
          <img
            src="../assets/image-product-1-thumbnail.jpg"
            alt="thumbnail one"
            @click="() => handleThumbnails('thumbnail one')"
            :class="
              option == 'thumbnail one' ? 'thumbnail_opaque' : 'thumbnail'
            "
          />
        </span>
        <span
          :class="
            option == 'thumbnail two' ? 'wrapper_active-border' : 'wrapper'
          "
        >
          <img
            src="../assets/image-product-2-thumbnail.jpg"
            alt="thumbnail two"
            @click="() => handleThumbnails('thumbnail two')"
            :class="
              option == 'thumbnail two' ? 'thumbnail_opaque' : 'thumbnail'
            "
          />
        </span>
        <span
          :class="
            option == 'thumbnail three' ? 'wrapper_active-border' : 'wrapper'
          "
        >
          <img
            src="../assets/image-product-3-thumbnail.jpg"
            alt="thumbnail three"
            @click="() => handleThumbnails('thumbnail three')"
            :class="
              option == 'thumbnail three' ? 'thumbnail_opaque' : 'thumbnail'
            "
          />
        </span>
        <span
          :class="
            option == 'thumbnail four' ? 'wrapper_active-border' : 'wrapper'
          "
        >
          <img
            src="../assets/image-product-4-thumbnail.jpg"
            alt="thumbnail four"
            @click="() => handleThumbnails('thumbnail four')"
            :class="
              option == 'thumbnail four' ? 'thumbnail_opaque' : 'thumbnail'
            "
          />
        </span>
      </span>
    </div>
    <div class="description__container">
      <small class="subtitle">sneaker company</small>
      <h1 class="title">fall limited edition sneakers</h1>
      <p class="pharse">
        these low-profile sneakers are your perfect casual wear companion.
        featuring a durable rubber outer sole, they'll whithstand everything the
        weather can offer.
      </p>
      <div class="button__container">
        <span class="text">
          <strong>$125.00 <small>50%</small></strong>
          <p>$250.00</p>
        </span>
        <span class="wrapper_button">
          <span class="plus__minus">
            <img
              src="../assets/icon-minus.svg"
              alt="icon minus"
              @click="handleCounterMinus"
            />
            <p>{{ counter }}</p>
            <img
              src="../assets/icon-plus.svg"
              alt="icon plus"
              @click="handleCounterPlus"
            />
          </span>
          <button class="cart__button" @click="handleTeste">
            <img src="../assets/icon-cart.svg" alt="icon cart" /> Add to cart
          </button>
        </span>
      </div>
    </div>
  </main>
</template>
