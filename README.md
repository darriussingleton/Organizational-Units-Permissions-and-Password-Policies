# Organizational-Units-Permissions-and-Password-Policies

<h2>File Share Setup and Testing</h2>

<h3>Part 1: Create and Configure Shared Folders on DC-1</h3>

<ol>
  <li>
    <p>Log into DC-1 as the domain admin account (<code>mydomain.com\jane_admin</code>).</p>
  </li>
  <li>
    <p>Create four folders on the <code>C:\</code> drive:</p>
    <ul>
      <li><code>read-access</code></li>
      <li><code>write-access</code></li>
      <li><code>no-access</code></li>
      <li><code>accounting</code></li>
    </ul>
  </li>
  <li>
    <p>Set permissions for the folders:</p>
    <ul>
      <li>
        <strong><code>read-access</code> folder:</strong>
        <ul>
          <li><strong>Group:</strong> <code>Domain Users</code></li>
          <li><strong>Permission:</strong> <code>Read</code></li>
        </ul>
      </li>
      <li>
        <strong><code>write-access</code> folder:</strong>
        <ul>
          <li><strong>Group:</strong> <code>Domain Users</code></li>
          <li><strong>Permission:</strong> <code>Read/Write</code></li>
        </ul>
      </li>
      <li>
        <strong><code>no-access</code> folder:</strong>
        <ul>
          <li><strong>Group:</strong> <code>Domain Admins</code></li>
          <li><strong>Permission:</strong> <code>Read/Write</code></li>
        </ul>
      </li>
      <li>
        <p>(Skip <code>accounting</code> for now)</p>
      </li>
    </ul>
  </li>
</ol>

<h3>Part 2: Access Shared Folders from Client-1</h3>

<ol>
  <li>
    <p>Log into Client-1 as a normal user (<code>mydomain\<someuser></code>).</p>
  </li>
  <li>
    <p>Navigate to the shared folder on DC-1:</p>
    <ul>
      <li>Open Run (Windows+R)</li>
      <li>Type <code>\\dc-1</code> and press Enter</li>
    </ul>
  </li>
  <li>
    <p>Attempt to access the created folders:</p>
    <ul>
      <li>
        <code>read-access</code> folder: You should be able to read files but not create or modify them.
      </li>
      <li>
        <code>write-access</code> folder: You should be able to read and write files.
      </li>
      <li>
        <code>no-access</code> folder: You should not be able to access this folder at all.
      </li>
    </ul>
    <p>Does it make sense?</p>
  </li>
</ol>

<h3>Part 3: Create and Test "ACCOUNTANTS" Security Group</h3>

<ol>
  <li>
    <p>Log back into DC-1 as <code>mydomain.com\jane_admin</code>.</p>
  </li>
  <li>
    <p>Create a new security group called <code>ACCOUNTANTS</code> in Active Directory.</p>
  </li>
  <li>
    <p>Set permissions for the <code>accounting</code> folder:</p>
    <ul>
      <li>
        <strong>Group:</strong> <code>ACCOUNTANTS</code>
      </li>
      <li>
        <strong>Permission:</strong> <code>Read/Write</code>
      </li>
    </ul>
  </li>
  <li>
    <p>Log back into Client-1 as <code>mydomain\<someuser></code>.</p>
  </li>
  <li>
    <p>Attempt to access the <code>accounting</code> folder in <code>\\DC-1\</code>. It should fail.</p>
  </li>
  <li>
    <p>Log out of Client-1.</p>
  </li>
  <li>
    <p>Log back into DC-1 as <code>mydomain.com\jane_admin</code>.</p>
  </li>
  <li>
    <p>Add <code>&lt;someuser&gt;</code> to the <code>ACCOUNTANTS</code> security group in Active Directory.</p>
  </li>
  <li>
    <p>Log back into Client-1 as <code>mydomain\<someuser></code> and try to access the <code>accounting</code> share in <code>\\DC-1\</code>. You should now be able to access it.</p>
  </li>
</ol>
