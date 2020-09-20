<script>
    let description = '';
    $: characters = description.length;
    $: words = description.split(' ').length;
    let notes = '';

    function handleSubmit(event){
        event.preventDefault();
        notes += event.explicitOriginalTarget[0].value + '. '
    }
</script>
<style>

</style>
<div>
    <form on:submit={handleSubmit}>
        <p>{notes}</p>
        <textarea bind:value={description} rows="5"></textarea>
        <input type="submit">
    </form>
    <p>Total characters : {characters}</p>
    <p>Total words : {words}</p>
</div>