<template>
    <div class="group-details" v-if="groupValue!=null" @click="edit()">
        <div class="head">
            {{groupValue.groupModel.title}}
        </div>
        <div class="details">
            <div class="qustion row" v-for="qValue in groupValue.questionValues.filter(q=>!hideEmptyQuestions || !q.isEmpty())">
                <span class="question-title col-md-3">
                    {{qValue.questionModel.title}}:
                </span>
                <span class="question-value col-md-9">
                    {{qValue.viewValue}}
                </span>
            </div>
        </div>
        <div class="modal fade" tabindex="-1" role="dialog" aria-hidden="true" ref="modal">
            <div class="modal-dialog modal-lg" role="document">
                <div class="modal-content">
                    <div class="modal-body">
                        <GroupComponent v-if="groupValue!=null" v-bind:group-value="groupValue"/>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-dismiss="modal"><i class="fa fa-times"></i>
                        </button>
                        <button type="button" class="btn btn-primary" @click="popUpOkClicked"><i
                                class="fa fa-check"></i></button>
                    </div>
                </div>
            </div>

        </div>
    </div>
</template>

<script>
    import GroupComponent from "../GroupComponent";

    export default {
        name: "GroupViewComponent",
        components: {GroupComponent},
        props: ['groupValue','hideEmptyQuestions'],
        methods: {
            edit() {
                $(this.$refs.modal).modal('show');
            },
            popUpOkClicked() {
                $(this.$refs.modal).modal('hide');
            }
        }
    }
</script>

<style scoped>
    .group-details:hover {
        box-shadow: 1px 1px 10px #000;
    }
    .group-details {
        border-bottom: 1px solid lightgray;
        padding: 20px 10px;
    }
    .head{
        padding:0 10px;
        font-size: larger;
    }
    .details{
        padding: 10px;

    }
    .question-title{
        color:gray;
    }
</style>