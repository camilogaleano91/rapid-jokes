<script>
    import AllEntitiesList from "../../components/AllEntitiesList.svelte";
    import {getAllVotings} from "../../axios/voting";
    import Navbar from "../../components/navigation/Navbar.svelte";
    import NoEntries from "../NoEntries.svelte";
    import { onMount } from "svelte";


    let votings = [];

    onMount(async () => {
        try {
            const votingsResult = await getAllVotings();
            votings = votingsResult;
        } catch (error) {
            console.error(`error when retreiving votings: ${error}`);
        }
    });

</script>

<Navbar />
<main>
    {#if votings.length > 0}
        <AllEntitiesList
        entity={votings}
        title="All Votings"
        firstColumn="For Joke"
        secondColumn="Voter"
        thirdColumn="Humor Rated"
        fourthColumn="Creativity Rated"
        fifthColumn="Voting Details"
        allVotings
        />
        {:else}
        <NoEntries entity="Votings" />
    {/if}
</main>