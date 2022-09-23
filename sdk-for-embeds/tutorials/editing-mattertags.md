# Editing Mattertags

### Adding a link to the description

The description supports the following markdown link format:

`[link text](link url)`

The following code snippets produces the image below it.

```typescript
sdk.Mattertag.editBillboard(mattertagSid, {
  description:"[Link to Matterport site!](https://www.matterport.com)",
});
```

<figure><img src="../../.gitbook/assets/description-link.png" alt=""><figcaption></figcaption></figure>

### Setting an image media source

We use embedly to present image media. We recommend that you verify your image url with the embedly explore display tool before setting it as a media source.

* Select your image url. For example we will use,

url: `https://static.matterport.com/mp_cms/media/filer_public/71/ca/71cabc75-99a5-41a4-917c-f45203f9254e/pro-21f8ddbae.png`

<figure><img src="../../.gitbook/assets/pro-21f8ddbae.png" alt=""><figcaption></figcaption></figure>

*   Verify your image is displayed correctly on the embedly explore display tool

    <figure><img src="../../.gitbook/assets/embedly-explore-display.png" alt=""><figcaption></figcaption></figure>
* Call [Mattertag.editBillboard](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mattertag#editbillboard) with the media source to update the billboard

```typescript
sdk.Mattertag.editBillboard(mattertagSid, {
  media: {
  type: sdk.Mattertag.MediaType.PHOTO,
  src: 'https://static.matterport.com/mp_cms/media/filer_public/71/ca/71cabc75-99a5-41a4-917c-f45203f9254e/pro-21f8ddbae.png',
});

```

<figure><img src="../../.gitbook/assets/mattertag-with-image.png" alt=""><figcaption></figcaption></figure>

### Setting a video media source

We use embedly to present video media. We recommend that you verify your video url with the embedly explore embed tool before setting it as a media source.

* Select your video url. For example we will use,

url: `https://www.youtube.com/watch?v=uO_x9TFNmTk`

<figure><img src="https://img.youtube.com/vi/uO_x9TFNmTk/0.jpg" alt=""><figcaption></figcaption></figure>

*   Verify your video is displayed correctly on the embedly explore embed tool

    <figure><img src="../../.gitbook/assets/embedly-explore-embed.png" alt=""><figcaption></figcaption></figure>
* Call [Mattertag.editBillboard](https://matterport.github.io/showcase-sdk/docs/reference/current/modules/mattertag#editbillboard) with the media source to update the billboard

```typescript
sdk.Mattertag.editBillboard(mattertagSid, {
  media: {
  type: sdk.Mattertag.MediaType.VIDEO,
  src: 'https://www.youtube.com/watch?v=uO_x9TFNmTk',
});
```

<figure><img src="../../.gitbook/assets/mattertag-with-video.png" alt=""><figcaption></figcaption></figure>
