<template>
    <div>
        <label for="" class="input-label">{{ text_input_top }}</label>
        <div class="input-group" style="flex-direction: column">
            <input type="url" pattern="^(http|https)://\.(.*)" class="input-all form-control ng-pristine ng-valid ng-touched" :class="status_value == false ? 'alert-input' : ''" v-model="valueUrl" v-on:input="pattern($event.target.value)" :maxlength="max" required />
            <div class="input-label-bottom" v-if="text_input_bottom != ''">{{ text_input_bottom }}</div>
            <div class="input-error" v-if="status_value == false">
                <font-awesome-icon :icon="['fa', icon_error]"></font-awesome-icon>
                Url ควรขึ้นต้นด้วย HTTP
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ["text_input_top", "text_input_bottom", "value", "status_value"],
    data() {
        return {
            icon_error: "exclamation",
            valueUrl : this.value,
            status : this.status_value,
            max: 255,
        };
    },
    watch: {
        value(val){
            this.valueUrl = val
        },
    },
    created() {},
    methods: {
        pattern(val) {
            if (val[0] && val[0] != "h" && val[0] != "H") {
                this.status = false;
                this.valueUrl = "";
            } else if (val[1] && val[1] != "t" && val[1] != "T") {
                this.status = false;
                this.valueUrl = "";
            } else if (val[2] && val[2] != "t" && val[2] != "T") {
                this.status = false;
                this.valueUrl = "";
            } else if (val[3] && val[3] != "p" && val[3] != "P") {
                this.status = false;
                this.valueUrl = "";
            } else {
                this.status = true;
                this.$emit("input", this.valueUrl);
            }

            // $emit("input", $event.target.value);
        },
    },
};
</script>
