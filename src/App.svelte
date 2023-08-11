<script>
  import {
    Table,
    Input,
    Button,
    Modal,
    ModalHeader,
    ModalBody,
    ModalFooter,
    FormGroup,
    Label,
    Form,
  } from "sveltestrap";
  import { createClient } from "@supabase/supabase-js";
  import { onMount } from "svelte";

  let users = [];
  1;

  const supabase = createClient(
    "https://qvjpkztrksxnaykmgwhx.supabase.co",
    "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InF2anBrenRya3N4bmF5a21nd2h4Iiwicm9sZSI6ImFub24iLCJpYXQiOjE2OTE3NTYwNzUsImV4cCI6MjAwNzMzMjA3NX0.oWfH3i0OVTW-hofhonBGOYhklrlsZRrUW9aM1JuNu9o"
  );

  let countries = [
    "Afghanistan",
    "Albania",
    "Algeria",
    "American Samoa",
    "Andorra",
    "Angola",
    "Anguilla",
    "Antarctica",
    "Antigua and Barbuda",
    "Argentina",
    "Armenia",
    "Aruba",
    "Australia",
    "Austria",
    "Azerbaijan",
    "Bahamas (the)",
    "Bahrain",
    "Bangladesh",
    "Barbados",
    "Belarus",
    "Belgium",
    "Belize",
    "Benin",
    "Bermuda",
    "Bhutan",
    "Bolivia (Plurinational State of)",
    "Bonaire, Sint Eustatius and Saba",
    "Bosnia and Herzegovina",
    "Botswana",
    "Bouvet Island",
    "Brazil",
    "British Indian Ocean Territory (the)",
    "Brunei Darussalam",
    "Bulgaria",
    "Burkina Faso",
    "Burundi",
    "Cabo Verde",
    "Cambodia",
    "Cameroon",
    "Canada",
    "Cayman Islands (the)",
    "Central African Republic (the)",
    "Chad",
    "Chile",
    "China",
    "Christmas Island",
    "Cocos (Keeling) Islands (the)",
    "Colombia",
    "Comoros (the)",
    "Congo (the Democratic Republic of the)",
    "Congo (the)",
    "Cook Islands (the)",
    "Costa Rica",
    "Croatia",
    "Cuba",
    "Curaçao",
    "Cyprus",
    "Czechia",
    "Côte d'Ivoire",
    "Denmark",
    "Djibouti",
    "Dominica",
    "Dominican Republic (the)",
    "Ecuador",
    "Egypt",
    "El Salvador",
    "Equatorial Guinea",
    "Eritrea",
    "Estonia",
    "Eswatini",
    "Ethiopia",
    "Falkland Islands (the) [Malvinas]",
    "Faroe Islands (the)",
    "Fiji",
    "Finland",
    "France",
    "French Guiana",
    "French Polynesia",
    "French Southern Territories (the)",
    "Gabon",
    "Gambia (the)",
    "Georgia",
    "Germany",
    "Ghana",
    "Gibraltar",
    "Greece",
    "Greenland",
    "Grenada",
    "Guadeloupe",
    "Guam",
    "Guatemala",
    "Guernsey",
    "Guinea",
    "Guinea-Bissau",
    "Guyana",
    "Haiti",
    "Heard Island and McDonald Islands",
    "Holy See (the)",
    "Honduras",
    "Hong Kong",
    "Hungary",
    "Iceland",
    "India",
    "Indonesia",
    "Iran (Islamic Republic of)",
    "Iraq",
    "Ireland",
    "Isle of Man",
    "Israel",
    "Italy",
    "Jamaica",
    "Japan",
    "Jersey",
    "Jordan",
    "Kazakhstan",
    "Kenya",
    "Kiribati",
    "Korea (the Democratic People's Republic of)",
    "Korea (the Republic of)",
    "Kuwait",
    "Kyrgyzstan",
    "Lao People's Democratic Republic (the)",
    "Latvia",
    "Lebanon",
    "Lesotho",
    "Liberia",
    "Libya",
    "Liechtenstein",
    "Lithuania",
    "Luxembourg",
    "Macao",
    "Madagascar",
    "Malawi",
    "Malaysia",
    "Maldives",
    "Mali",
    "Malta",
    "Marshall Islands (the)",
    "Martinique",
    "Mauritania",
    "Mauritius",
    "Mayotte",
    "Mexico",
    "Micronesia (Federated States of)",
    "Moldova (the Republic of)",
    "Monaco",
    "Mongolia",
    "Montenegro",
    "Montserrat",
    "Morocco",
    "Mozambique",
    "Myanmar",
    "Namibia",
    "Nauru",
    "Nepal",
    "Netherlands (the)",
    "New Caledonia",
    "New Zealand",
    "Nicaragua",
    "Niger (the)",
    "Nigeria",
    "Niue",
    "Norfolk Island",
    "Northern Mariana Islands (the)",
    "Norway",
    "Oman",
    "Pakistan",
    "Palau",
    "Palestine, State of",
    "Panama",
    "Papua New Guinea",
    "Paraguay",
    "Peru",
    "Philippines (the)",
    "Pitcairn",
    "Poland",
    "Portugal",
    "Puerto Rico",
    "Qatar",
    "Republic of North Macedonia",
    "Romania",
    "Russian Federation (the)",
    "Rwanda",
    "Réunion",
    "Saint Barthélemy",
    "Saint Helena, Ascension and Tristan da Cunha",
    "Saint Kitts and Nevis",
    "Saint Lucia",
    "Saint Martin (French part)",
    "Saint Pierre and Miquelon",
    "Saint Vincent and the Grenadines",
    "Samoa",
    "San Marino",
    "Sao Tome and Principe",
    "Saudi Arabia",
    "Senegal",
    "Serbia",
    "Seychelles",
    "Sierra Leone",
    "Singapore",
    "Sint Maarten (Dutch part)",
    "Slovakia",
    "Slovenia",
    "Solomon Islands",
    "Somalia",
    "South Africa",
    "South Georgia and the South Sandwich Islands",
    "South Sudan",
    "Spain",
    "Sri Lanka",
    "Sudan (the)",
    "Suriname",
    "Svalbard and Jan Mayen",
    "Sweden",
    "Switzerland",
    "Syrian Arab Republic",
    "Taiwan",
    "Tajikistan",
    "Tanzania, United Republic of",
    "Thailand",
    "Timor-Leste",
    "Togo",
    "Tokelau",
    "Tonga",
    "Trinidad and Tobago",
    "Tunisia",
    "Turkey",
    "Turkmenistan",
    "Turks and Caicos Islands (the)",
    "Tuvalu",
    "Uganda",
    "Ukraine",
    "United Arab Emirates (the)",
    "United Kingdom of Great Britain and Northern Ireland (the)",
    "United States Minor Outlying Islands (the)",
    "United States of America (the)",
    "Uruguay",
    "Uzbekistan",
    "Vanuatu",
    "Venezuela (Bolivarian Republic of)",
    "Viet Nam",
    "Virgin Islands (British)",
    "Virgin Islands (U.S.)",
    "Wallis and Futuna",
    "Western Sahara",
    "Yemen",
    "Zambia",
    "Zimbabwe",
    "Åland Islands",
  ];

  let gender;

  let entries = 10;

  let open = false;

  const toggle = () => {
    open = !open;
  };

  const load = async () => {
    const { data, error } = await supabase.from("users").select("*");

    if (error) {
      alert(error.message);
    } else {
      users = data;
    }
  };

  const submit = async () => {
    let avatar = null;

    const reader = new FileReader();
    if (document.getElementById("avatar").files[0]) {
      reader.readAsDataURL(document.getElementById("avatar").files[0]);
      while (reader.result === null) {
        await new Promise((resolve) => setTimeout(resolve, 100));
      }

      avatar = reader.result;
    }
    let firstName = document.getElementById("firstName").value;
    let lastName = document.getElementById("lastName").value;
    let email = document.getElementById("email").value;
    let country = document.getElementById("country").value;

    const count = await supabase
      .from("users")
      .select("*", { count: "exact", head: true });

    let id = count.count ? count.count + 1 : 1;

    const error = await supabase.from("users").insert({
      id: id,
      first_name: firstName,
      last_name: lastName,
      email: email,
      avatar: avatar,
      country: country,
      gender: gender,
    });

    if (error.error) {
      alert(error.error.message);
    } else {
      load();
      toggle();
    }
  };

  onMount(() => {
    load();
  });
</script>

<div>
  <h4><strong>All users</strong></h4>
  <p>Manage all your existing users or add a new one</p>

  <div>
    <span>Show</span>
    <Input
      type="number"
      name="number"
      id="entries"
      placeholder=""
      style="width: 8em; display: inline;"
      bind:value={entries}
    />
    <span>entries</span>
  </div>
</div>

<Button color="primary" on:click={toggle}>Add new user</Button>

<Modal isOpen={open} {toggle}>
  <ModalHeader {toggle}>Add users</ModalHeader>
  <ModalBody>
    <Form>
      <FormGroup style="width: 45%; display: inline-block; margin-right: 5%;">
        <Label for="firstName">First Name</Label>
        <Input
          type="text"
          name="firstName"
          id="firstName"
          placeholder="First Name"
        />
      </FormGroup>
      <FormGroup style="width: 45%; display: inline-block;">
        <Label for="lastName">Last Name</Label>
        <Input
          type="text"
          name="lastName"
          id="lastName"
          placeholder="Last Name"
        />
      </FormGroup>
      <FormGroup>
        <Label for="email">Email</Label>
        <Input type="email" name="email" id="email" placeholder="Email" />
      </FormGroup>
      <FormGroup>
        <Label for="avatar">Avatar</Label>
        <Input type="file" name="avatar" id="avatar" />
      </FormGroup>
      <FormGroup>
        <Label for="country">Country</Label>
        <Input type="select" name="country" id="country">
          {#each countries as country}
            <option>{country}</option>
          {/each}
        </Input>
      </FormGroup>
      <FormGroup>
        <Label for="gender">Gender</Label>
        <Input
          type="radio"
          id="male"
          bind:group={gender}
          value="Male"
          label="Male"
        />
        <Input
          type="radio"
          id="female"
          bind:group={gender}
          value="Female"
          label="Female"
        />
      </FormGroup>
    </Form>
  </ModalBody>
  <ModalFooter>
    <Button color="primary" on:click={submit}>Submit</Button>
    <Button color="secondary" on:click={toggle}>Cancel</Button>
  </ModalFooter>
</Modal>

<Table>
  <thead>
    <tr>
      <th>#</th>
      <th>First Name</th>
      <th>Last Name</th>
      <th>Image</th>
      <th>Email</th>
      <th>Country</th>
      <th>Gender</th>
    </tr>
  </thead>

  <tbody>
    {#each users as user}
      <tr>
        <th scope="row">{user.id}</th>
        <td>{user.first_name}</td>
        <td>{user.last_name}</td>
        <td
          ><img
            src={user.avatar}
            alt={user.first_name}
            style="width: 2em; height: 2em;"
          /></td
        >
        <td>{user.email}</td>
        <td>{user.country}</td>
        <td>{user.gender}</td>
      </tr>
    {/each}
  </tbody>
</Table>
