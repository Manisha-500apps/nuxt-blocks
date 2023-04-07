<template>
  <div>
    <div>
      <CollectionList :units="units"></CollectionList>
    </div>
    <div>
      <CollectionAdd @add_units="addUnits"></CollectionAdd>
      <CollectionEdit @add_units="addUnits"></CollectionEdit>
    </div>
    <div></div>
  </div>
</template>
<script lang="ts" setup>
const getOptions = {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
    Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiNGEyZTI0MWQ5YzEyNDAzMjgzODQ0NzNmOTFiMWFkYzEiLCJkIjoiMTY4MDExNyIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODM0Mzc1OTl9.BG5jHROYJfR1Hxg7KgDas_-4IbuGHNT_k5xW7b1b4D4`,
  },
};
const units = await useAuthLazyFetch(
  " https://v1-orm-lib.mars.hipso.cc/blocks/?offset=0&limit=100&sort_column=id&sort_direction=desc",
  getOptions
);

// Add Template to the template data
function addUnits(data: object) {
  const postOptions = {
    body: JSON.stringify(data),
  };

  useAuthLazyFetchPost("https://v1-orm-lib.mars.hipso.cc/blocks/", postOptions);
}
function deletUnits(data: object) {
  const postOptions = {
    body: JSON.stringify(data),
  };

  useAuthLazyFetchDelete(
    `https://v1-orm-lib.mars.hipso.cc/blocks/${uid}`,
    postOptions
  );
}
</script>
