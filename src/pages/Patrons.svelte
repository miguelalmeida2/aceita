<script>
  import PatronCard from "../components/PatronCard.svelte";

  let patrons = [];

  async function fetchPatrons() {
    const url = `https://raw.githubusercontent.com/talvasconcelos/aceita/main/patrons.json`;
    try {
      const response = await fetch(url);
      if (!response.ok) throw new Error("Patrons not found");
      return await response.json();
    } catch (error) {
      console.error(`Error fetching Patrons:`, error);
    }
  }

  // Fetch and order meetups on component initialization
  fetchPatrons().then((fetchedPatrons) => {
    patrons = fetchedPatrons.patrons;
  });
</script>

<section class="container grid-lg">
  <header>
    <h2>Apoiantes</h2>
    <div class="subtitle">
      <p>Descubra as pessoas que apoiam o nosso trabalho</p>
    </div>
  </header>
  <section class="container grid-lg">
    <div cl>
      {#each patrons as patron, i}
        <PatronCard
          patronName={patron.patronName}
          patronService={patron.patronService}
          contact={patron.contact}
          description={patron.serviceDescription}
          img={patron.img}
          buttonURL={patron.website}
          buttonText="Saber Mais"
          img_right
        />
      {/each}
    </div>
  </section>
</section>

<style>
  .quote {
    text-align: center;
    width: 100%;
    font-size: 1.2rem;
    font-weight: 300;
    padding: 1rem 0;
  }
  @media (min-width: 600px) {
    .quote {
      font-size: 1.5rem;
    }
  }
</style>
