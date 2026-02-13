# Sanity Blog CMS

A content management system built with Sanity.io for managing blog posts with rich text editing capabilities.

## Prerequisites

Before you begin, ensure you have the following installed:
- Node.js (v18 or higher)
- npm or yarn package manager
- A Sanity account (sign up at [sanity.io](https://www.sanity.io))

## Installation

1. Clone the repository:
```bash
git clone <your-repository-url>
cd sanity-blog-cms
```

2. Install dependencies:
```bash
npm install
```

## Configuration

### Create a Sanity Project

1. If you don't have a Sanity project yet, create one:
```bash
npm create sanity@latest -- --project <project-name> --dataset production
```

2. Or use an existing Sanity project and get your project ID from the [Sanity Management Console](https://www.sanity.io/manage).

### Environment Variables

Create a `.env` file in the root directory and add your Sanity project credentials:

```env
SANITY_STUDIO_PROJECT_ID=your_project_id_here
SANITY_STUDIO_DATASET=production
```

To find these values:
- **Project ID**: Available in your Sanity project settings at [sanity.io/manage](https://www.sanity.io/manage)
- **Dataset**: Usually `production` or `development`

## Running the CMS

### Development Mode

Start the Sanity Studio in development mode with hot-reloading:
```bash
npm run dev
```

The CMS will be available at `http://localhost:3333`

### Production Build

Build the Sanity Studio for production:
```bash
npm run build
```

### Start Production Server

Start the production server:
```bash
npm start
```

## Features

### Blog Post Content Type

The CMS includes a Blog Post content type with the following fields:

- **Title**: The blog post title (required)
- **Slug**: URL-friendly identifier (auto-generated from title)
- **Author**: Post author name (required)
- **Main Image**: Featured image with hotspot support (required)
- **Published Date**: Publication date and time (required)
- **Body**: Rich text content with support for:
  - Paragraphs
  - Headings
  - Lists
  - Block quotes
  - Images
  - And more

### Plugins

- **Structure Tool**: Organize and manage your content
- **Vision**: Query your content using GROQ (Graph-Relational Object Queries)

## Usage

### Creating a New Blog Post

1. Navigate to the Sanity Studio (default: `http://localhost:3333`)
2. Click on "Blog Post" in the sidebar
3. Click the "+ Create" button
4. Fill in all required fields:
   - Enter a title
   - Generate a slug (click "Generate" button)
   - Add author name
   - Upload a main image
   - Set the publication date
   - Write your blog content in the body editor
5. Click "Publish" to save your blog post

### Using GROQ Queries

Access the Vision tool to query your content:
1. Click on "Vision" in the top navigation
2. Write GROQ queries to fetch your blog posts

Example queries:
```groq
// Get all published blog posts
*[_type == "blogPost"] | order(publishedAt desc)

// Get a specific blog post by slug
*[_type == "blogPost" && slug.current == "your-slug"][0]

// Get recent posts with specific fields
*[_type == "blogPost"] | order(publishedAt desc) [0...5] {
  title,
  slug,
  author,
  publishedAt,
  "imageUrl": mainImage.asset->url
}
```

## Project Structure

```
sanity-blog-cms/
├── schemas/              # Content schema definitions
│   ├── index.ts         # Schema exports
│   └── blogPost.ts      # Blog post schema
├── sanity.config.ts     # Sanity configuration
├── sanity.cli.ts        # Sanity CLI configuration
├── tsconfig.json        # TypeScript configuration
└── package.json         # Project dependencies
```

## Deployment

### Deploy to Sanity

Deploy your Sanity Studio to be hosted by Sanity:
```bash
npx sanity deploy
```

You'll be prompted to choose a studio hostname. Your studio will be available at:
`https://your-studio-name.sanity.studio`

## API Access

To access your content via API in your frontend application:

1. Install the Sanity client:
```bash
npm install @sanity/client
```

2. Configure the client:
```javascript
import {createClient} from '@sanity/client'

const client = createClient({
  projectId: 'your-project-id',
  dataset: 'production',
  useCdn: true,
  apiVersion: '2024-01-01',
})

// Fetch blog posts
const posts = await client.fetch('*[_type == "blogPost"]')
```

## Additional Resources

- [Sanity Documentation](https://www.sanity.io/docs)
- [GROQ Query Language](https://www.sanity.io/docs/groq)
- [Sanity Schema Types](https://www.sanity.io/docs/schema-types)
- [Sanity Community](https://www.sanity.io/community)

## License

ISC

## Support

For issues and questions:
- Check the [Sanity documentation](https://www.sanity.io/docs)
- Visit the [Sanity Community Slack](https://slack.sanity.io/)
