<template>
    <nav class="c-nav">
        <span> {{ companyName }}</span>
      <ul class="c-nav-list">
        <li class="c-nav-list-item" v-for="(link, index) in links" v-bind:key="index">
            <a v-bind:href="link.linkUrl" v-bind:target="link.target">{{ link.linkText }}</a>
        </li>
        
      </ul>
    </nav>
</template>

<script>
export default {
    name: 'Navigation',
    data() {
        return {
            companyName: 'Eurovision Song Contest',
            links: [
                {
                    linkText: "Home",
                    linkUrl: "/home",
                    target: "_blank"
                },
                {
                    linkText: "Shop",
                    linkUrl: "/shop",
                    target: "_blank"
                },
                {
                    linkText: "Contact",
                    linkUrl: "/contact",
                    target: "_blank"
                }
                
                ]

            
        }
    }
}
</script>