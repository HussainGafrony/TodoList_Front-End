<template>
    <div>
       <v-col class="mt-8">
        <v-row v-for="(item, index) in item" :key="index"  dense justify="center">
            <v-checkbox class="pt-2" v-model="item.completed" @change="updateCheck()"></v-checkbox>
            <v-hover v-slot="{ hover }">
                <v-col cols="12" md="4">
                    <v-card :elevation="hover ? 12 : 2" :class="{ 'on-hover': hover }"
                        color="#385F73" dark rounded="pill" @reloadlist="$emit('reloadlist')">
                        <v-card-title class="text-h6 headerClass pl-2" :class="[
                          item.completed ? 'text-decoration-line-through red--text' : '',
                        ]">
                            {{ item.name }}
                        </v-card-title>
                    </v-card>
                    <p class="mt-4"><v-icon>mdi-message-off-outline</v-icon></p>
                    <v-expand-transition>
                        <div v-if="hover" class="black--text font-weight-bold">
                            {{ item.name }}
                        </div>
                    </v-expand-transition>
                </v-col>
            </v-hover>
            <v-btn small color="error" dark fab elevation="1" class="mx-4 my-3" @click="removeItem()">
                <v-icon> mdi-delete </v-icon>
            </v-btn>
        </v-row>
       </v-col>
    </div>
</template>
<script>
import axios from "axios";

export default {
    name: "show_todo",
    props: ["item"],
    methods: {
        updateCheck() {
            axios
                .put("http://127.0.0.1:8000/api/item/" + this.item[0].id, {})
                .then(() => { })
                .catch((error) => {
                    console.log(error);
                });
        },
        removeItem() {
            axios
                .delete("http://127.0.0.1:8000/api/" + this.item[0].id, {})
                .then((result) => {
                    if (result.status == 200) {
                        this.$emit("delete-todo");
                    }
                })
                .catch((error) => {
                    console.log(error);
                });
        },
    },
};
</script>

<style scoped>
.v-card--reveal {
    align-items: center;
    bottom: 0;
    justify-content: center;
    opacity: 0.5;
    position: absolute;
    width: 100%;
}

.headerClass {
    white-space: nowrap;
    word-break: normal;
    overflow: hidden;
    text-overflow: ellipsis;
    display: block;
}
</style>
