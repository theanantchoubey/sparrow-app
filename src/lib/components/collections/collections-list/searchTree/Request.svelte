<script lang="ts">
  import { replaceSlashWithGreaterThanSymbol } from "$lib/utils/helpers/common.helper";
  import { getMethodStyle } from "$lib/utils/helpers/conversion.helper";
  import { handleRequestClick } from "$lib/utils/helpers/handle-clicks.helper";
  export let path: string = "";
  export let searchData: string = "";
  export let getIndex;
  export let folderDetails: { id: string; name: string };
  export let request: any;
  export let workspaceId: string = "";
  export let collectionId: string = "";
</script>

<div
  class="d-flex align-items-center api-request p-1"
  style="height: {path !== '' ? '40px' : '32px'};"
  on:click={() => {
    handleRequestClick(request, {
      collectionId,
      workspaceId,
      folderId: folderDetails.id ? folderDetails.id : "",
      folderName: folderDetails.name ? folderDetails.name : "",
    });
  }}
>
  <div class="api-method text-{getMethodStyle(request.request.method)}">
    {request.request.method.toUpperCase()}
  </div>
  <div class="api-name" style="width:80%;">
    <div>
      <p class="mb-0 ellipsis" style="color:#999999;">
        {request.name.substring(0, getIndex(request.name, searchData))}<span
          class="highlight"
          >{request.name.substring(
            getIndex(request.name, searchData),
            getIndex(request.name, searchData) + searchData.length,
          )}</span
        >{request.name.substring(
          getIndex(request.name, searchData) + searchData.length,
        )}
      </p>
    </div>
    {#if path !== ""}
      <div style="width: 100%;">
        <p class="mb-0 ellipsis" style="font-size:10px;width:100%">
          {replaceSlashWithGreaterThanSymbol(path)}
        </p>
      </div>
    {/if}
  </div>
</div>

<style>
  .red-api {
    color: var(--request-delete);
  }
  .green-api {
    color: var(--request-get);
  }
  .yellow-api {
    color: var(--request-post);
  }
  .blue-api {
    color: var(--request-put);
  }
  .grey-api {
    color: var(--request-arc);
  }
  .api-method {
    font-size: 12px;
    font-weight: 500;
    margin-right: 8px;
    text-align: left;
  }
  .api-name p {
    font-size: 12px;
    font-weight: 400;
  }
  .highlight {
    color: var(--white-color);
  }
  .api-request {
    width: 100%;
    height: 60px;
  }
</style>
