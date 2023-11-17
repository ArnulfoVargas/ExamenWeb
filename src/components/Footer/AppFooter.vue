<script setup>
    import FooterIcon from './FooterIcon.vue';
    import FooterSocial from "./FoooterSocial.vue"
    import uniqid from "uniqid"

    const socialMedias = [
        {
            name: "Itch.io",
            image: "/FooterLogos/itchio.svg",
            link: "https://arnulfodev.itch.io/"
        },
        {
            name: "GitHub",
            image: "/FooterLogos/github.svg",
            link: "https://github.com/ArnulfoVargas"
        },
        {
            name: "Linkedin",
            image: "/FooterLogos/linkedin.svg",
            link: "https://www.linkedin.com/in/arnulfo-vargas-mej%C3%ADa/"
        }
    ]
</script>

<template>
    <div class="footer-container">
        <FooterIcon/>

        <div class="social-container">
            <FooterSocial
                v-for="(social) in socialMedias"
                :data="social"
                :key="uniqid()"
            />
        </div>
    </div>
</template>

<style>
    .footer-container{
        background-color: var(--color-gray);
        width: calc(100% - 5rem);
        height: fit-content;
        padding: 2.5rem;
        display: flex;
        flex-direction: column;
        gap: 2.5rem;
        justify-content: space-between;
        align-items: center;
    }

    .social-container{
        width: fit-content;
        margin: auto;
        display: flex;
        gap: 1rem;
    }

    @media (min-width: 768px) {
        .footer-container{
            gap: 0;
            flex-direction: row;
        }

        .social-container{
            width: fit-content;
            margin: 0;
        }
    }
</style>