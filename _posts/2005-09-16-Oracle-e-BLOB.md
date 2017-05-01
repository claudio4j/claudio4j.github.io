---
id: 85
title: Oracle e BLOB
date: 2005-09-16T15:58:05+00:00
author: Claudio Miranda
layout: post
permalink: /2005/09/Oracle-e-BLOB/
categories:
  - Java
---
Resolvi a pouco um problema que me importunava h&aacute; alguns dias, era com o uso de BLOB em oracle.

Basicamente, o que tenho na aplica&ccedil;&atilde;o é um objeto java que quero serializar em BLOB e depois l&ecirc;-lo, mas resultava nos seguintes erros:

<font size="3" color="red"></p> 

<pre>
java.io.IOException: Message [ORA-4283276] not found in 'oracle.jdbc.dbaccess.Messages'.
        at oracle.jdbc.dbaccess.DBError.SQLToIOException(DBError.java:717)
        at oracle.jdbc.driver.OracleBlobInputStream.needBytes(OracleBlobInputStream.java:249)
        at oracle.jdbc.driver.OracleBufferedStream.read(OracleBufferedStream.java:158)
        at java.io.ObjectInputStream$PeekInputStream.read(ObjectInputStream.java:2150)
        at java.io.ObjectInputStream$PeekInputStream.readFully(ObjectInputStream.java:2163)
        at java.io.ObjectInputStream$BlockDataInputStream.readShort(ObjectInputStream.java:2631)
        at java.io.ObjectInputStream.readStreamHeader(ObjectInputStream.java:734)
        at java.io.ObjectInputStream.&lt;init>(ObjectInputStream.java:253)
        at claudius.Serial56.writeAndReadSetBinary(Blob56.java:111)
        at claudius.Serial56.main(Blob56.java:399)
        # =========================================================
java.sql.SQLException: ORA-21608: duration is invalid for this function

        at oracle.jdbc.dbaccess.DBError.throwSqlException(DBError.java:134)
        at oracle.jdbc.oci8.OCIDBAccess.check_error(OCIDBAccess.java:2355)
        at oracle.jdbc.oci8.OCIDBAccess.createTemporaryLob(OCIDBAccess.java:3678)
        at oracle.jdbc.dbaccess.DBAccess.createTemporaryLob(DBAccess.java:1355)
        at oracle.sql.LobDBAccessImpl.createTemporaryBlob(LobDBAccessImpl.java:373)
        at oracle.sql.BLOB.createTemporary(BLOB.java:778)
        at claudius.SerialBase.buildBlob(SerialBase.java:205)
        at claudius.Serial56.writeAndReadBLOBCreateTemporary(Blob56.java:151)
        at claudius.Serial56.main(Blob56.java:405)
        # =========================================================
java.io.IOException: Message [ORA-4282764] not found in 'oracle.jdbc.dbaccess.Messages'.
        at oracle.jdbc.dbaccess.DBError.SQLToIOException(DBError.java:717)
        at oracle.jdbc.driver.OracleBlobInputStream.needBytes(OracleBlobInputStream.java:249)
        at oracle.jdbc.driver.OracleBufferedStream.read(OracleBufferedStream.java:158)
        at oracle.jdbc.driver.OracleBufferedStream.read(OracleBufferedStream.java:131)
        at claudius.Serial56.writeAndReadInsertEmpty(Blob56.java:284)
        at claudius.Serial56.main(Blob56.java:412)

</pre>

<p>
  </font>
</p>

<p>
  A vers&atilde;o do Oracle era 9.2.0.6 (dispon&iacute;vel apenas no <a targte="_blank" href="http://metalink.oracle.com">metalink.oracle.com</a>), ent&atilde; o ambiente foi atualizado para o 9.2.0.7 (&uacute;ltimo da s&eacute;rie 9.2.x), mesmo porque no release notes n&atilde;o indicava nenhuma corre&ccedil;&atilde;o espec&iacute;fica do erro que apresentava para mim.
</p>

<p>
  O conselho ent&atilde;o &eacute;: atualize a vers&atilde;o do Oracle para a mais recente
</p>