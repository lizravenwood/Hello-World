<!DOCTYPE html>
<html>
<body>

<?php
include ('simple_html_dom.php');

// this does a simple scrape of just the first title and image
echo "Beginning to scrape...<br>\n";
$websiteurl = "https://uuctucson.org";

$html = file_get_html($websiteurl);

$urls = array();
// Find all <li> in <ul>
foreach($html->find('ul') as $ul)
{
       foreach($ul->find('li') as $li)
       {
         foreach($li->find('a') as $a)
         //echo $a->attr['href']. "<br>";
         $urls [] = $a->attr['href'];
       }
}

echo "<br>done scraping, now loading up into an array<br>\n";
echo "<br>length of the array BEFORE sort and cleanup is ".sizeof($urls)."<br><br>";
$myfile = fopen("newfile.txt", "w") or die("Unable to open file!");
// sort the array
sort($urls);
array($dataout)->$urls;

for($idx=1;$idx<=count($urls)-1;$idx++)
{
  //echo "item ".$idx." is ".$urls[$idx]."<br>";
  //echo "search loc is ".strpos($urls[$idx],"javascript")."<br>";
  if (strpos($urls[$idx],"javascript")===false) // apparently if it exists the index is greater than 0
  {
  fwrite($myfile, $urls[$idx] . "\n");
  $dataout[$idx]=$urls[$idx];
  }

}

echo "<br>length of the array AFTER the sort and cleanup is ".sizeof($dataout)."<br><br>";

fclose($myfile);

echo "cleaned results are in the file newfile.txt";
?>
</body>
</html>
