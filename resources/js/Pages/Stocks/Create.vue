<template>
    <div>
        <Layout>
            <div class="flex justify-center w-full">
                <div class="bg-white flex flex-col w-1/3 mt-20 p-6">
                    <h2 class="text-lg">Stock Form</h2>
                    <form
                        id="stock-form"
                        name="stock-form"
                        v-on:submit.prevent="submit"
                    >
                        <div class="flex flex-col pt-6">
                            <label for="id">ID</label>
                            <input
                                type="text"
                                id="id"
                                name="id"
                                v-model="form.id"
                                autocomplete="off"
                            />
                            <div class="text-red-700 text-sm">
                                {{ errors.id }}
                            </div>
                            {{ form.id }}
                        </div>

                        <div class="flex flex-col pt-6">
                            <label for="description">Description</label>
                            <input
                                type="text"
                                id="description"
                                name="description"
                                v-model="form.description"
                                autocomplete="off"
                            />
                            <div class="text-red-700 text-sm">
                                {{ errors.description }}
                            </div>
                        </div>

                        <div class="flex flex-col pt-6">
                            <label for="stock_category_id">Stock Category ID</label>
                            <select name="stock_category_id" id="stock_category_id" v-model="form.stock_category_id">
                                <option value="7962">7962</option>
                                <option value="44780">44780</option>
                                <option value="19778">19778</option>
                                <option value="35908">35908</option>
                                <option value="46251">46251</option>
                                <option value="39738">39738</option>
                                <option value="46989">46989</option>
                                <option value="21330">21330</option>
                                <option value="15204">15204</option>
                                <option value="58075">58075</option>
                                <option value="3436">3436</option>
                                <option value="63387">63387</option>
                                <option value="38081">38081</option>
                                <option value="56042">56042</option>
                                <option value="58380">58380</option>
                                <option value="63367">63367</option>
                                <option value="3858">3858</option>
                                <option value="34795">34795</option>
                                <option value="32756">32756</option>

                            </select>

                            <div class="text-red-700 text-sm">
                                {{ errors.stock_category_id }}
                            </div>
                        </div>

                        <div class="flex flex-col pt-6">
                            <label for="uom">UOM</label>
                            <select name="uom" id="uom" v-model="form.uom">
                                <option value="BND">BND</option>
                                <option value="PK">PK</option>
                                <option value="GAL">GAL</option>
                                <option value="BX">BX</option>
                                <option value="CS">CS</option>
                                <option value="RL">RL</option>
                                <option value="DZ">DZ</option>
                                <option value="CTN">CTN</option>
                                <option value="CRD">CRD</option>
                                <option value="CM">CM</option>
                                <option value="MM">MM</option>
                                <option value="BAG">BAG</option>
                                <option value="BKT">BKT</option>
                            </select>

                            <div class="text-red-700 text-sm">
                                {{ errors.uom }}
                            </div>
                        </div>

                        <div class="flex flex-col pt-6">
                            <label for="description">Barcode</label>
                            <input
                                type="text"
                                id="barcode"
                                name="barcode"
                                v-model="form.barcode"
                                autocomplete="off"
                            />
                            <div class="text-red-700 text-sm">
                                {{ errors.barcode }}
                            </div>
                        </div>

                        <div class="flex flex-col pt-6">
                            <label for="type">Discontinued
                            <input class="ml-2" type="checkbox" id="yes" true-value="Y" false-value="N" v-model="form.discontinued">
                            <label class="ml-2" for="yes">Yes</label>
                            <input class="ml-4" type="checkbox" id="no" true-value="N" false-value="Y" v-model="form.discontinued">
                            <label class="ml-2" for="no">No</label>
                            <br>
                            </label>

                            <div class="text-red-700 text-sm">
                                {{ errors.discontinued }}
                            </div>
                        </div>


                        <div class="flex flex-col pt-6">
                            <button
                                type="submit"
                                class="bg-indigo-800 text-white p-2"
                            >
                                Save
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </Layout>
    </div>
</template>

<script>
import { ref, reactive } from "vue";
import Layout from "@/Layouts/Authenticated";
import { Inertia } from "@inertiajs/inertia";
export default {
    components: {
        Layout,
    },
    props: {
        errors: Object,
    },
    setup(props, context) {
        const form = reactive({
            id: null,
            description: null,
            stock_category_id: "7962",
            uom: "BND",
            barcode: null,
            discontinued: "Y",
           

        });
        const submit = () => {
            Inertia.post(route("stock.store"), form, {
               onSuccess: () => {
                    // Handle success event
                    form.id = null;
                    form.description = null;
                    form.stock_category_id = "7962";
                    form.uom = "BND";
                    form.barcode = null;
                    form.discontinued = "Y";
                    //   this.reset();
                },
            });
        };
        return {
            form,
            submit,
        };
    },
};
</script>