The [OpenCann.net gateway](https://opencann.net) is a [Next.js](https://nextjs.org/) app that renders [React](https://react.dev/) components from [Near Protocol](https://near.org) using the [Near Social VM](https://github.com/NearSocial/VM).

# Browser

A framework for reusable components to render and modify SocialDB by Near Social.

## Setup & Development

Initialize repo:
```
yarn
```

Start development version:
```
yarn start
```

## Widget example

Profile view 

```jsx
let accountId = props.accountId || "eugenethedream";
let profile = socialGetr(`${accountId}/profile`);

(
  <div>
    <img src={profile.image.url}/>
    <span>{profile.name}</span> <span>(@{accountId})</span>
  </div>
);
```


Profile editor 

```jsx
let accountId = context.accountId;

if (!accountId) {
  return "Please sign in with NEAR wallet";
}

const profile = socialGetr(`${accountId}/profile`);

if (profile === null) {
  return "Loading";
}

initState({
  name: profile.name,
  url: profile.image.url,
});

const data = {
  profile: {
    name: state.name,
    image: {
      url: state.url,
    },
  },
};

return (
  <div>
    <div>account = {accountId}</div>
    <div>
      Name:
      <input type="text" value={state.name} />
    </div>
    <div>
      Image URL:
      <input type="text" value={state.url} />
    </div>
    <div>Preview</div>
    <div>
      <img src={state.url} alt="profile image" /> {state.name}
    </div>
    <div>
      <CommitButton data={data}>Save profile</CommitButton>
    </div>
  </div>
);

```
