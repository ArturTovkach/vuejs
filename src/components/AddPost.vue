<template>
    <form @submit.prevent="createPost()" :class="{error: maxCharacters > 20}">
            <label for="title">Название статьи:</label>
            <input v-model="state.userTitleInput" type="text" id="title" placeholder="Введите название статьи">
            <label for="title">Основной текст: <span>{{ maxCharacters }} / 20</span></label>
            <textarea v-model="state.userTextInput" id="text" placeholder="Введите текст" ></textarea>
            <button >Добавить</button>
        </form>
</template>

<script>
import { reactive, computed} from 'vue';

export default{
    name: 'AddPost',

    setup(props, ctx){
        const state = reactive({
            userTitleInput: '',
            userTextInput: '',
        })

        const maxCharacters = computed(() => state.userTextInput.length);

        const createPost = () => {
            if(state.userTitleInput !== '' && state.userTextInput !== ''){
                ctx.emit('add-post', state.userTitleInput, state.userTextInput)
                
                state.userTextInput = '';
                state.userTitleInput = '';
            }
        }

        return {
            state,
            maxCharacters,
            createPost
        }
    }
}
</script>

<style>
form{
    margin-top: 20px;
}

form label{
    color: #505050;
}

 form input,
 form textarea {
    width: 100%;
    background: #c6c391;
    border-radius: 5px;
    border: 2px solid #5e5b21;
    padding: 8px 10px;
    font-size: 14px;
    color: #5e5b21;
    outline: none;
    margin-bottom: 10px;
    resize: none;
}

 form.error label{
    color: #d73838;
}

form button{
    float: right;
    background: #aaa771;
    border: 2px solid #5e5b21;
    border-bottom-width: 4px;
    padding: 10px 12px;
    font-size: 13px;
    font-weight: bold;
    color: #5e5b21;
    border-radius: 5px;
    cursor: pointer;
    transition: all 500ms ease;
}

form button:hover{
    margin-top: 2px;
    border-bottom-width:2px ;
}


</style>