<script>

   export let title;
   export let width;

</script>

<style>
   h2 {
      font-family: "akkurat",sans-serif;
       font-size: 1.8rem;
       font-weight: 700;
       letter-spacing: unset;
       text-transform: unset;
       border-top: unset;
       border-bottom: unset;
       line-height: unset;
       padding: unset;
   }

   svg {
      margin:0 auto;
      display:block;
   }
</style>

<h2 class="graphictitle">{title}</h2>
<svg width="330" height="30">
   <g>
      <rect
         fill="#841e77"
         width="80"
         height="25"
      >
      </rect>
      <text
         x="2"
         y="18"
         text-anchor="start"
         font-family="Flaticon"
         fill="white"
      >
         &#xf101;
      </text>
      <text
         x="25"
         y="17"
         text-anchor="start"
         fill="white"
         font-size="13px"
      >
         driving
      </text>
   </g>
   <g transform="translate(85,0)">
      <rect
         fill="#02acac"
         width="80"
         height="25"
      >
      </rect>
      <text
         x="2"
         y="18"
         text-anchor="start"
         font-family="Flaticon"
         fill="white"
      >
         &#xf102;
      </text>
      <text
         x="25"
         y="17"
         text-anchor="start"
         fill="white"
         font-size="13px"
      >
         walking
      </text>
   </g>
   <g transform="translate(170,0)">
      <rect
         fill="#d51e2d"
         width="160"
         height="25"
      >
      </rect>
      <text
         x="2"
         y="18"
         text-anchor="start"
         font-family="Flaticon"
         fill="white"
      >
         &#xf100;
      </text>
      <text
         x="25"
         y="17"
         text-anchor="start"
         fill="white"
         font-size="13px"
      >
         public transportation
      </text>
   </g>
</svg>
<!-- <span class="graphicsubhed">{subhed}</span> -->
