<template>
    <button :class="ButtonClasses">
        <slot></slot>
    </button>
</template>

<script>
    export default{
    props: {
        type: {
                type: String,
                default: 'primary'
            },
            isMenCloth: {
                type: Boolean,
                default: false
            },
            isWomenCloth: {
                type: Boolean,
                default: false
            },
            isProductButton: {
                type: Boolean,
                default: false
            }
    },
    computed: {
            ButtonClasses() {
                const classes = ['button'];
                
                if(this.isButtonProduct){
                    classes.push('btn-main')
                }

                if(this.type === 'primary'){
                    if(this.isMenCloth){
                        classes.push('btn-primary-blue')
                    }else if(this.isWomenCloth){
                        classes.push('btn-primary-purple')
                    }else{
                        classes.push('btn-primary-dark')
                    }
                }else if(this.type === 'primary-outline'){
                    if(this.isMenCloth){
                        classes.push('btn-primary-outline-blue')
                    }else if(this.isWomenCloth){
                        classes.push('btn-primary-outline-purple')
                    }else{
                        classes.push('btn-primary-outline-dark')
                    }
                }else{
                    classes.push('btn-outline-black')
                }

                return classes;
            }
        }
}
</script>

<style scoped>
   .button{
        width: 260px;
        height: 42px;
        font-size: 20px;
        font-style: normal;
        font-weight: 600;
        line-height: normal;
        border-radius: 4px;
        border: none;
        cursor: pointer;
        position: relative;
        text-decoration: none;
        transition: all 250ms;
        user-select: none;
        -webkit-user-select: none;
        touch-action: manipulation;
        vertical-align: baseline;
        box-shadow: rgba(0, 0, 0, 0.02) 0 1px 3px 0;
    }

    .btn-main{
        width: 450px;
    }

    /* Button Purple */
    .btn-primary-purple{
        background-color: var(--primary-purple);
        color: var(--color-white);
    }

    .btn-primary-outline-purple{
        background-color: var(--color-white);
        border: 3px solid var(--primary-purple);
        color: var(--primary-purple);
    }

    .btn-primary-purple:hover{
        background-color: var(--primary-purple-inactive);
        box-shadow: rgba(0, 0, 0, 0.1) 0 4px 12px;
        transform: translateY(-1px);

    }

    .btn-primary-outline-purple:hover{
        background-color: var(--primary-purple-inactive);
        border-color: var(--primary-purple-inactive);
        color: #ffffff;
        box-shadow: rgba(0, 0, 0, 0.1) 0 4px 12px;
        transform: translateY(-1px);
    }

    /* Button Blue */
    .btn-primary-blue{
        background-color: var(--primary-blue);
        color: var(--color-white);
    }

    .btn-primary-outline-blue{
        background-color: var(--color-white);
        border: 3px solid var(--primary-blue);
        color: var(--primary-blue);
    }

    .btn-primary-blue:hover{
        background-color: var(--primary-blue-inactive);
        box-shadow: rgba(0, 0, 0, 0.1) 0 4px 12px;
        transform: translateY(-1px);

    }

    .btn-primary-outline-blue:hover{
        background-color: var(--primary-blue-inactive);
        border-color: var(--primary-blue-inactive);
        color: #ffffff;
        box-shadow: rgba(0, 0, 0, 0.1) 0 4px 12px;
        transform: translateY(-1px);
    }

    /* Button Dark */
    .btn-outline-black{
        background-color: #fff;
        border: 3px solid #000;
        color: #000;
    }

    .btn-outline-black:hover{
        background-color: #000;
        border-color: #000;
        color: #ffffff;
        box-shadow: rgba(0, 0, 0, 0.1) 0 4px 12px;
        transform: translateY(-1px);
    }

    @media only screen and (max-width: 600px) {
        .btn-large {
            font-size: 14px;
            width: 250px;
        }
    }

</style>