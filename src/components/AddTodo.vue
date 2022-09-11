<template>
    <app>
        <v-row class="pt-15" justify="center">
            <v-col cols="12" md="5">
                <v-row>
                    <v-text-field height="28" clearable
                        class="grey black--text font-italic font-weight-bold"
                        color="black" placeholder="Write Todo" rounded v-model="name" label="Todo">
                    </v-text-field>
                    <v-icon class="ml-2" large @click="Addtodo()" :class="[name ? 'active' : 'inactive'] ">
                        mdi-plus
                    </v-icon>
                </v-row>
            </v-col>
        </v-row>
    </app>

</template>

<script>
import Axios from 'axios';
export default {
    name: "Add_Todo",
    data: () => ({
        name: "",

    }),
    methods: {
        Addtodo() {
            if (this.name == "") {
                return;
            }

            Axios.post("http://127.0.0.1:8000/api/store", {
                name: this.name,
            })
                .then((response) => {
                    if (response.status == 201) {
                        this.name = "";
                        this.$emit('add-todo');
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
.active {
    color: green;
}

.inactive {
    color: #E0E0E0;
}
</style>
