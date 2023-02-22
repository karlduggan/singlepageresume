<template>
    <transition name="fade">
        <div class="modal" v-show="open">
            <div class="inner-modal">
                <div class="content-modal">
                    <div class="content">
                        <slot/>
                    </div>
                    
                    
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
    export default {
        props: {
            open: {
                type: Boolean,
                required: true
            }
        }
    }
</script>

<style scoped>
    ::before,
    ::after {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
    .modal {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        overflow-x: hidden;
        overflow-y: auto;
        background-color: rgb(0,0,0, 0.5);
        z-index: 1;
    }
    .inner-modal {
        max-width: 500px;
        margin: 2rem auto;
    }
    .content-modal {
        position: relative;
        background-color: #fff;
        background-clip: border-box;
        border: 1px solid rgb(0,0,0, 0.3);
        padding: 2rem;
    }
    .content {
        justify-content: center;
    }
    .fade-enter-active,
    .fade-leave-active {
        transition: opacity 0.5s;
    }
    .fade-enter,
    .fade-leave-to {
        opacity: 0;
    }
 
 
  
</style>