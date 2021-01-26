<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="title">Todo List App</h2>
            <add-item-form v-on:reloadlist="getList()" />
        </div>
        <list-view :items="items" v-on:reloadlist="getList()" />
    </div>
</template>
<script>
import addItemForm from "./addItemForm";
import listView from "./listView";

export default {
    components: {
        addItemForm,
        listView
    },
    data: function() {
        return {
            items: []
        };
    },
    methods: {
        getList() {
            axios
                .get("api/items")
                .then(response => {
                    this.items = response.data;
                })
                .catch(error => {
                    console.log(error);
                });
        }
    },
    created() {
        this.getList();
    }
};
</script>
<style scoped>
.todoListContainer {
    width: 350px;
    margin: auto;
}
.heading {
    background: #e4b5b5;
    padding: 10px;
}

#title {
    text-align: center;
}
</style>
