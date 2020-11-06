<template>
    <transition name="modal">
    <div class="modal_wrapper" @click="$emit(close)">
        <div class="modal-content" @click.stop="">

            <!--header -->
            <div class="modal-header">
                <span class="modal-title">{{ title }} </span>
                <span class="button-close" @click="$emit(close)">x</span>
            </div>

            <!-- body -->
            <div class="modal-body">
                <slot name="body"> Default body </slot>
            </div>
        </div>
    </div>
    </transition>  
</template>

<script>
export default {
    props: {
        title: {
            type: String,
            required: true
        }
    },
    data () {
        return {}
    },
    mounted () {
        document.body.addEventListener('keyup', e => {
            if (e.keyCode === 27) this.$$emit('close')
        })
    },
    computed: {},
    methods: {}
}
</script>

<style lang="scss" scoped>
// animation
.modal-enter, .modal-leave-active {
    opacity: 0;
}
.modal-enter, .modal-content,
.modal-leave-active .modal-content{
    transform: scale(1.2);
}

.modal_wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    transition: opacity .3s ease;
    right: 0;
    z-index: 998;
    background-color: rgba($color: #000000, $alpha: 1.0);
}

.modal-content {
    position: relative;
    max-width: 600px;
    padding: 20px 18px;
    background-color: #fff;
    border: 1px solid #dcdfe6;
    transition: all .3s ease;
    border-radius: 8px;
    z-index: 999;
    overflow: hidden;
}

.modal-header {
    display: flex;
    align-self: center;
    justify-content: space-between;
    padding-bottom: 20px;
    span {
        font-size: 24px;
    }
    .button-close {
        cursor: pointer;
    }
}

.modal-body {
    text-align: center;
}

</style>