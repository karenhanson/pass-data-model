# Deposit

A [Submission](Submission.md) can have multiple Deposits, each to a different [Repository](Repository.md). This entity describes the interaction of PASS with a target [Repository](Repository.md) for an individual [Submission](Submission.md) with the purpose of satisfying one or more [Policies](Policy.md).

| Field  		   | Type  	| Description
| ---------------- | ------ | ------------- 
| __id*__          | URI    | Unique Deposit URI (autogenerated)
| depositStatusRef | String | A URL or some kind of reference that can be dereferenced, entity body parsed, and used to determine the status of Deposit
| depositStatus*   | Enum   | Status of deposit ([_see list below_](#deposit-status-options))
| submission*      | URI    | URI of [Submission](Submission.md) this Deposit is a part of
| repository*      | URI    | URI of the [Repository](Repository.md) being deposited to 
| repositoryCopy   | URI    | URI of the [Repository Copy](RepositoryCopy.md) representing the copy that is reltaed to this Deposit. The value is null if there is no copy
 
*required 

*Properties automatically generated by the system are documented in [System Properties](SystemProperties.md). These are not available to client tools by default.*

## Deposit status options

These are the possible statuses for a Deposit in the order they could occur. Note that not all repositories will go through every status.

<dl>
  <dt>Intermediate status</dt>
  <dd>A Deposit with an <em>intermediate</em> status indicates that the processing of the Deposit is not yet
      complete.  At some indeterminate point in the future, the status <em>may</em> be updated to a <em>terminal</em>
      state.
  </dd>
  <dt>Terminal status</dt>
  <dd>A Deposit with a <em>terminal</em> status indicates that the processing of the Deposit is complete.
  </dd>
</dl>

| Value     | State        | Description 
| --------- | -----        | ---
| submitted | Intermediate | PASS has sent a package to the target [Repository](Repository.md) and is waiting for an update on the status
| rejected  | Terminal     | The target [Repository](Repository.md) has rejected the Deposit
| failed    | Intermediate | A failure occurred while performing the deposit, it may be re-tried later.
| accepted  | Terminal     | The target [Repository](Repository.md) has accepted the [Files](File.md) into the repository and they are pending publication if not published already
