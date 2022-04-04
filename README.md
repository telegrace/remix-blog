# Remix

```sh
npx create-remix --template remix-run/indie-stack blog-tutorial
```

```
? Do you want me to run `npm install`? Yes
...
? Do you want to run the build/tests/etc to verify things are setup properly? Yes
```

```sh
remix setup
```

**Doesn't work, but you still need to manually install remix ** `npm i remix`

```sh
npm run dev
```

### Routes

Routes are similar to file structure in next.js and old HTML files

### Dynamic Routes

```sh
app/routes/posts/\$slug.tsx
```

### Index Routes (nested routes)

Every route inside of `app/routes/posts/admin/` can now render _inside_ of `app/routes/posts/admin.tsx` when their URL matches. You get to control which part of the `admin.tsx` layout the child routes render.

Just know that when the URL matches the parent route's path, the index will render inside the `outlet`.

### Relative Links

```
<Link to="admin" className="text-red-600 underline">
  Admin
</Link>
```

The `to` prop is just "admin" and links to /posts/admin?

### Loaders

` const { posts } = useLoaderData() as LoaderData;`

Loaders can be moved to `models/post/post.server.ts `

and we get type safety across the network

```
type LoaderData = {
  // this is a handy way to say: "posts is whatever type getPosts resolves to"
  posts: Awaited<ReturnType<typeof getPosts>>;
};
```

```
type LoaderData = { post: Post };
```

### Actions

`useActionData` is just like `useLoaderData` but the data comes from the action after a form POST.

# Prisma

```sh
npx prisma db push
```

Add the info for seeding in the seed function in seed.ts

```
npx prisma db seed
```

If you change Prisma you need to change restart the server

    ### Notes

` ~/db.server`

~ refers app folder

Because `params` comes from the URL, we can't be totally sure that `params.slug` will be defined--maybe you change the name of the file to `$postId.ts`! It's good practice to validate that stuff with `invariant`
