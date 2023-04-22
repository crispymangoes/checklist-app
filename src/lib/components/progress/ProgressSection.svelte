<script>
    import ProgressBar from "./ProgressBar.svelte";
    import { todos } from "../../store/TodoStore"

    export let completePercentage = 0;
    export let progressPercentage = 0;

    $: totalCount = $todos.length;
    $: completeCount = $todos.filter((todo) => todo.complete).length;
    $: progressCount = $todos.filter((todo) => !todo.complete).length;
    $: completePercentage = Math.round((completeCount / totalCount) * 100) || 0;
    $: progressPercentage = Math.round((progressCount / totalCount) * 100) || 0;
    // The || is an or so if the Math number is undefined it uses a fallback of zero
</script>

<section class="mt-10">
    <h3 class="text-xl font-bold text-gray-three">Progress</h3>
    <div class="mt-8 space-y-8">
        <ProgressBar title="In Progress" percentage={progressPercentage} />
        <ProgressBar title="Completed" percentage={completePercentage} />
    </div>
</section>