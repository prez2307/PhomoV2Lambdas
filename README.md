# Phomo V2 Lambdas

Lambda function handlers for Phomo V2 backend infrastructure.

## Structure

```
src/
├── face-processing/       # Face detection, enrollment, matching
├── api-resolvers/         # AppSync GraphQL resolvers
├── stream-processing/     # DynamoDB stream handlers
└── scheduled-jobs/        # EventBridge cron jobs
```

## Lambda Functions

### Face Processing (3)
- `process-content-faces.ts` - Detect and match faces in uploaded photos (SQS trigger)
- `enroll-face.ts` - Enroll user face for profile (AppSync mutation)
- `retroactive-match.ts` - Match unknown faces when friendship accepted

### API Resolvers (3)
- `accept-friendship.ts` - Accept friend request + trigger retroactive matching
- `get-content-url.ts` - Generate presigned S3 URLs for content
- `find-friends-by-phone.ts` - Contact discovery by phone numbers

### Stream Processing (1)
- `feed-entry-sync.ts` - Sync FeedEntry when RecipientEdge created (DynamoDB Stream)

### Scheduled Jobs (1)
- `send-event-reminders.ts` - Send event reminders hourly (EventBridge cron)

## Development

```bash
npm install
npm run build
```

## Deployment

These Lambda functions are deployed via the PhomoV2CDK infrastructure repository.
The CDK pipeline automatically pulls this repo and bundles the TypeScript handlers.
