<template>
    <div class="container-fluid" id="demo">
        <div class="col-md-6 col-md-offset-3 mt20">

            <div class="form-horizontal">

                <div class="form-group">
                    <div class="col-sm-12">
                        <div class="alert alert-info"><i class="glyphicon glyphicon-cog mr5"></i>快速选择
                        </div>
                    </div>
                </div>
                <div class="form-group">
                    <div class="col-sm-12 setting-group">
                        <button type="button" class="btn btn-sm btn-default"
                                :class="{ 'btn-success': setting.selected }"
                                v-for="(setting, index) in quickSettings"
                                @click="set(setting, index)">{{ setting.name }}
                        </button>
                    </div>
                </div>

                <hr class="dashed mt-30 mb-30">

                <div class="form-group">
                    <div class="col-sm-6">
                        <div class="input-group">
                            <span class="input-group-addon">RegExp</span>
                            <input type="text" class="form-control" disabled
                                   v-model="setting.regExp">
                        </div>
                    </div>
                </div>
                <div class="form-group">
                    <div class="col-sm-6">
                        <div class="input-group">
                            <span class="input-group-addon">Replacement</span>
                            <input type="text" class="form-control" disabled
                                   v-model="setting.replacement">
                        </div>
                    </div>
                </div>

                <hr class="dashed mt-30 mb-30">

                <div class="form-group">
                    <div class="col-sm-12">
                        <div class="alert alert-success"><i class="glyphicon glyphicon-arrow-down mr5"></i>试一试
                        </div>
                    </div>
                </div>
                <div class="form-group">
                    <div class="col-sm-12">
                        <pattern-input class="form-control" maxlength="11" placeholder="maxlength 11"
                                       :regExp="setting.regExp"
                                       :replacement="setting.replacement"
                                       @input="handleInput"
                                       @change="handleChange"
                                       v-model="setting.val"></pattern-input>
                    </div>
                </div>
                <div class="form-group">
                    <div class="col-sm-12">
                        <pre>得到的数据：{{ setting.val }}</pre>
                    </div>
                </div>
                <div class="form-group">
                    <div class="col-sm-12">
                        <button type="button" class="btn btn-danger" @click="clearInput">clear input</button>
                    </div>
                </div>

            </div>

        </div>
    </div>
</template>

<script type="text/ecmascript-6">
    import PatternInput from '../../../../component/ct-adc-pattern-input.vue';

    export default {
        components: {
            PatternInput
        },
        data () {
            return {
                setting: {
                    regExp: /^[0\D]*|\D*/g,
                    replacement: '',
                    val: 'awdawd123'
                },
                quickSettings: [
                    {
                        name: 'Noting',
                        regExp: null,
                        replacement: '',
                        selected: false
                    },
                    {
                        name: 'Positive Integer',
                        regExp: /^[0\D]*|\D*/g,
                        replacement: '',
                        selected: true
                    },
                    {
                        name: 'Lowercase',
                        regExp: /[^a-z]/g,
                        replacement: '',
                        selected: false
                    },
                    {
                        name: 'Chinese',
                        regExp: /[^\u4e00-\u9fa5]/g,
                        replacement: '',
                        selected: false
                    },
                    {
                        name: 'Phone Number (Need set [maxlength = 11])',
                        regExp: /^[^1]|\D*/g,
                        replacement: '',
                        selected: false
                    }
                ]
            };
        },
        methods: {
            set (oSetting, nIndex) {
                this.setting.regExp = oSetting.regExp;
                this.setting.replacement = oSetting.replacement;

                this.setSelectedStatus(nIndex);
                this.clearInput();
            },
            setSelectedStatus (nIndex) {
                this.quickSettings.map((setting, index) => {
                    if (nIndex === index) {
                        setting.selected = true;
                    } else {
                        setting.selected = false;
                    }

                    return true;
                });
            },
            clearInput() {
                this.setting.val = '';
            },
            handleInput(val) {
                console.log(`input: ${ val }`);
            },
            handleChange(val) {
                console.log(`change: ${ val }`);
            }
        }
    }
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
    .setting-group {
        .btn + .btn {
            margin-left: 5px;
        }
    }

    .dashed {
        border-style: dashed;
    }

    .mt-30 {
        margin-top: 30px;
    }

    .mb-30 {
        margin-bottom: 30px;
    }
</style>