<template>
    <div 
        :style="{
            backgroundColor: products[index].color
        }"
        class="products"
    >

        <!-- Nav -->
        <div class="products__nav">

            <!-- Opener -->
            <button type="button" class="products__nav-opener"></button>

            <!-- Title -->
            <h1 class="products__nav-title">"Spot"</h1>

            <div class="products__nav-cart">{{ products.filter(p => p.added).length }}</div>

        </div>

        <!-- Content -->
        <div class="products__content">

            <!-- Subtitle -->
            <h4 class="products__content-subtitle">New drop</h4>

            <!-- Title -->
            <transition mode="out-in" name="slideout">
                <h3 :key="index" class="products__content-title">{{ products[index].title }}</h3>
            </transition>

            <!-- CTA -->
            <button 
                @click="products[index].added = !products[index].added" 
                type="button" 
                :class="['products__content-cta', {added: products[index].added}]"
                >{{products[index].added ? 'Remove now' : 'Shop now'}}</button>

        </div>

        <!-- Pagination -->
        <div class="products__pagination">
            <button 
                v-for="(product, i) in products" 
                :key="product.title"
                @click="index = i"
                :class="['products__pagination-link', {active: i === index}]"
            >{{ i + 1 }}</button>
        </div>

    </div>
</template>

<script>
import Product from "../models/Product"

export default {
    name: "Products",
    props: {},
    data: function(){
        return {
            index: 0,
            products: [
                new Product("Nike Air Presto \n Off-White", "#d35400"),
                new Product("Nike Air \n Jordan 1", "#f1c40f"),
                new Product("Nike Air \n Max 97", "#16a085"),
            ]
        }
    }
}
</script>

<style lang="scss" scoped>
    .products{

        .slideout-enter-active, .slideout-leave-active {
            transition: ease-out .35s;
            transition-property: transform, opacity;
        }
        .slideout-enter, .slideout-leave-to /* .slideout-leave-active below version 2.1.8 */ {
            transform: translate(0, 12px);
            opacity: 0;
        }

        // Variables
            // Size
            $pagination-link-size: 24px;
            $pagination-link-color: #363636;

        display: flex;
        flex-direction: column;
        font-family: Arial, Helvetica, sans-serif;
        height: 100%;
        transition: background-color ease .35s;
        padding: 20px 24px;

        // Nav
        &__nav{
            display: flex;
            align-items: center;

            &-opener{
                width: 40px;
                height: 40px;
                background-color: #000;
                color: #fff;
                border-radius: 100%;
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
                border: none;

                &:after, &:before{
                    content: "";
                    background-color: rgba(255, 255, 255, .6);
                    height: 2px;
                    width: 60%;
                    display: inline-block;
                    margin: 2px 0;
                }
            }

            &-title{
                font-size: 30px;
                margin: 0 auto;
                text-transform: uppercase;
                font-weight: 700;
            }

            &-cart{
                width: 40px;
                height: 40px;
                border: 2px solid rgba(0, 0, 0, .6);
                border-radius: 100%;
                text-align: center;
                line-height: 35px;
                font-weight: 700;
            }
        }

        // Content
        &__content{
            text-align: center;
            margin-top: 30vh;

            &-subtitle{
                text-transform: uppercase;
                font-size: 12px;
                letter-spacing: -.02em;
                margin-bottom: 32px;
            }

            &-title{
                font-family: 'Times New Roman', Times, serif;
                font-size: 52px;
                font-weight: 100;
                letter-spacing: -.02em;
                max-width: 350px;
                margin: 0 auto;
                margin-bottom: 28px;
                white-space: pre-line;
            }

            &-cta{
                border: none;
                background-color: #000;
                border: 2px solid #000;
                color: #fff;
                text-transform: uppercase;
                font-weight: 700;
                font-size: 11px;
                height: 46px;
                width: 150px;
                border-radius: 40px;
                text-decoration: none;
                display: inline-block;
                cursor: pointer;

                &.added{
                    background-color: transparent;
                    color: #000;
                }
            }
        }

        // Pagination
        &__pagination{
            text-align: center;
            margin-top: auto;

            &-link{
                border: 2px solid $pagination-link-color;
                color: $pagination-link-color;
                background: none;
                border-radius: 100%;
                width: $pagination-link-size;
                height: $pagination-link-size;
                text-align: center;
                font-weight: 700;
                font-size: 11px;
                margin: 0 4px;
                cursor: pointer;
                opacity: .35;
                transition: opacity ease .35s;

                &.active{
                    opacity: 1;
                }
            }
        }
    }
</style>