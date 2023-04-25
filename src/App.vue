<script setup lang="ts">
  import BackgroundImages from "@/components/BackgroundImages.vue";
  import Section from "@/components/Section.vue";
  import TitleHr from "@/components/TitleHr.vue";
  import CountryPercentageChart from "@/components/CountryPercentageChart.vue";
  import EmissionsOverTimeVue from "@/components/EmissionsOverTimeChart.vue";
  import FooterImage from "@/assets/footer.svg";
  import ViewOnGithubButton from "@/components/ViewOnGithubButton.vue";
</script>

<template>
  <main>
    
    <ViewOnGithubButton/>

    <Section id="head-section">

      <h1>Visualizing Global Emissions</h1>

      <p>
          With the current global warming crisis, visualizing the scale of the issue at the local and nation-state level is a helpful tool for cultivating an informed urgency on the matter.<br/><br/>
          Using data from <a href='https://www.climatewatchdata.org'>climatewatchdata.org</a> this page aims to draw attention to the carbon emissions of countries and how they are changing over time.
      </p>

    </Section>
    
    <Section>  
      <TitleHr :sideLineHeight="2">
        <h2>CO<sub>2</sub> Emissions By Country</h2>
      </TitleHr>
    </Section>
    
    <CountryPercentageChart/>

    <Section>
      <p>
        Since 2005, China has had the highest CO<sub>2</sub> emissions of any country. 
        This data can be misleading though, because on a per-capita basis, the U.S. has 14.7 metric tons per-capita compared to China's 7.6 metric tons per-capita.
      </p>
    </Section>

    <Section>
      <TitleHr :sideLineHeight="2">
        <h2>CO<sub>2</sub> Emissions Over Time</h2>
      </TitleHr>
    </Section>

    <EmissionsOverTimeVue/>

    <Section>
      <p>
        While developed nations CO<sub>2</sub> emissions have steadied and in some places began to level off, emissions in developing nations are still growing (though at a slowing rate).
      </p>
    </Section>

    <BackgroundImages/>
    <img id="footer-img" :src="FooterImage"/>

  </main>
</template>

<style>
#main-time{
  height: 200vh;
  width: 100%;
}

#head-section{
  flex-direction: column;
  padding-top: 2em;
}

#footer-img{
  width: 100%;
  opacity: 0.2;
  transform: translateY(5px);
}
</style>


