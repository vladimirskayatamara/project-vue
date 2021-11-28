<template>
  <div class="product">
    <div v-on:click="() => onDelete(data.id)" class="delete-wrap">
      <div class="delete-icon"></div>
    </div>
    <img :src="data.image" :alt="data.name" class="product-image" />
    <div class="product-info">
      <p class="product-name">{{ data.name }}</p>
      <p class="product-description">{{ data.description }}</p>
      <p class="product-price">{{ formattedPrice }} руб.</p>
    </div>
  </div>
</template>
<script>
import { formatPrice } from "../utils/utils";
export default {
  props: {
    data: Object,
    onDelete: Function,
  },
  computed: {
    formattedPrice() {
      return formatPrice(this.data.price);
    },
  },
};
</script>

<style lang="less" scoped>
.product {
  transition: all 1s;
  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  cursor: pointer;
  position: relative;
  min-width: 332px;
  max-width: 332px;
  margin-right: 16px;
  margin-bottom: 16px;
  min-height: 423px;

  &:nth-child(3n){
    margin-right: 0;  
  }

  &:hover {
    .delete-wrap {
      display: block;
    }
  }
}
.delete-wrap {
  display: none;
  position: absolute;
  width: 32px;
  height: 32px;
  background: #ff8484;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  padding: 8px;
  top: 0px;
  right: -8px;
}
.delete-icon {
  width: 13px;
  height: 16px;
  background-repeat: no-repeat;
  background-size: contain;
  background-position: center;
  background-image: url("~/assets/images/delete.png");
}

.product-image {
  object-fit: cover;
  width: 100%;
  max-height: 200px;
  border-radius: 4px 4px 0 0;
}
.product-info {
  padding: 11px 16px 16px 16px;
}
.product-name {
  font-style: normal;
  font-weight: 600;
  font-size: 20px;
  line-height: 25px;
  color: #3F3F3F;
  margin-bottom: 16px;
  overflow: hidden;
  text-overflow: ellipsis;
}
.product-description {
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 20px;
  color: #3F3F3F;
  margin-bottom: 32px;
  overflow: hidden;
  text-overflow: ellipsis;
}
.product-price{
  font-style: normal;
  font-weight: 600;
  font-size: 24px;
  line-height: 30px;
  color: #3F3F3F;
}

</style>